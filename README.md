# MNIST

Deep learning pattern recognition on the famous mnist dataset [mnist dataset](http://yann.lecun.com/exdb/mnist/).

Dataset consists of 60.000 training samples and 10.000 test samples of hand-drawn digits of size 28x28 single channel pixels.

## Framework

All examples are trained and tested within the [caffe franework](caffe.berkeleyvision.org/).

Custom layers will be noted with and asterisk.

## Preprocessing 

* Pixels are scaled from [0 256] to [-1 +1].

* Randomly zeroing pixels out with 1% probability

* Cropping window of 25x25

## Regularization

* weight decay 

## Linear Classifier - Baseline

Every pixel is a feature.

Accuracy after 500k iterations 0.925 ~ error 7.5%

Number of parameters SoftMax(A*x + b) => (25*25) * 10 + 10= 6260

```
name: "MNIST_NET"
############################
layer {
  name: "data"
  type: "ImageData"
  top: "data"
  top: "label"
  include {
    phase: TRAIN
  }
  image_data_param {
    is_color : false
    shuffle : true
    source: "train.txt"
    batch_size: 200
    crop_size : 25
  }
}
layer {
  name: "data"
  type: "ImageData"
  top: "data"
  top: "label"
  include {
    phase: TEST
  }
  image_data_param {
    is_color : false
    shuffle : true
    source: "test.txt"
    batch_size: 100
    crop_size : 25
  }
}
############################
## Preprocessing
## Scale from [0-255] [-1 +1]
layer {
  name: "data/scaling"
  type: "Power"
  bottom: "data"
  top: "data"
  power_param {
    power: 1
    scale: 0.0078125
    shift: -1.0
  }
}

layer {
  name: "data/drop"
  type: "Dropout"
  bottom: "data"
  top: "data"
  dropout_param {
    dropout_ratio: 0.01
  }
  include {
    phase: TRAIN
  }
}
############################
layer {
  name: "fc_10"
  type: "InnerProduct"
  bottom: "data"
  top: "fc_10"
  param {
    lr_mult: 5
    decay_mult: 1
  }
  param {
    lr_mult: 10
    decay_mult: 0
  }
  inner_product_param {
    num_output: 10
    weight_filler {
      type: "gaussian"
      std: 0.01
    }
    bias_filler {
      type: "constant"
      value: 0
    }
  }
}
############################
layer {
  name: "loss"
  type: "SoftmaxWithLoss"
  bottom: "fc_10"
  bottom: "label"
  top: "loss"
  include {
    phase: TRAIN
  }
}
layer {
  name: "accuracy"
  type: "Accuracy"
  bottom: "fc_10"
  bottom: "label"
  top: "accuracy"
  include {
    phase: TEST
  }
}
```
