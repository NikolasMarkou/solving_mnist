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

### Notes

Accuracy after 500k iterations 0.925 ~ error 7.5%

Number of parameters : 6260

## 2 Layer Neural Network Classifier with PreLU

### Notes

Accuracy after 500k iterations 0.983 ~ error 1.17%
