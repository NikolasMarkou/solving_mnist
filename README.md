# MNIST

Deep learning pattern recognition on the famous mnist dataset [mnist dataset](http://yann.lecun.com/exdb/mnist/).

Dataset consists of 60.000 training samples and 10.000 test samples of hand-drawn digits of size 28x28 single channel pixels.

![Some of mnist samples](images/mnist.png)

## Framework

All examples are trained and tested within the [caffe franework](caffe.berkeleyvision.org/).

Custom layers will be noted with and asterisk.

## Preprocessing 

* Pixels are scaled from [0 256] to [-1 +1].

* Randomly zeroing pixels out with 1% probability

* Cropping window of 25x25

## Regularization

* weight decay 

## [Linear Classifier - Baseline](models/linear_classifier.prototxt)

### Notes

Accuracy after 500k iterations 0.925 ~ error 7.5%

Number of parameters : 6260

## [2 Layer Neural Network Classifier with ReLU](models/2_layer_NN_relu.prototxt.prototxt)

### Notes

Accuracy after 500k iterations 0.983 ~ error 1.17%

## [2 Layer Neural Network Classifier with PReLU](models/2_layer_NN_prelu.prototxt)

### Notes

Accuracy after 500k iterations 0.983 ~ error 1.17%

Faster convergence than ReLU

## [3 Layer Neural Network 256 - 128 - 10 with PReLu](models/3_layer_NN_256_128_10.prototxt)

### Notes

Accuracy after 500k iterations 0.986 ~ error 1.14%

## [3 Layer Neural Network 256 - 128 - 10 with PReLU and dataset expansion layer](models/3_layer_NN_256_128_10_with_dataset_expansion.prototxt)

### Notes

This one uses the custom dataset expansion layer that randomly transforms the input with noise and affine transformations

Accuracy after 500k iterations 0.9912 ~ error 0.88%

## [2 Layer CNN (36 kernels 3x3 stride 2) (28 kernels 3x3 stride 1) with PReLU and dataset expansion](models/cnn_2_layer_dataset_expansion.prototxt)

### Notes

This one uses the custom dataset expansion layer that randomly transforms the input with noise and affine transformations

Accuracy after 3 x 500k iterations 0.9935 ~ error 0.65%


## [3 Layer CNN (64 kernels 3x3 stride 1) (256 kernels 3x3 stride 2) (64 kernels 3x3 stride 2) with PReLU and dataset expansion](models/cnn_3_layer_with_dataset_expansion.prototxt)

### Notes

This one uses the custom dataset expansion layer that randomly transforms the input with noise and affine transformations

Accuracy after 3 x 500k iterations 0.9945 ~ error 0.55%
