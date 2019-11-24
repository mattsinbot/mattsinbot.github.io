---
title: "Machine Learning Projects"
permalink: /mlprojects/
header:
  # image: "/images/deeplearning.jpg"
---

### LASSO Regression for Feature Selection
Least Absolute Shrinkage and Selection Operator or LASSO is a regression method, highly used in Machine learning community for determining important features when number of features are lot more than needed. We have solved LASSO regression problem using synthetic data that finds only 10 important features out of 80 given features that are required to predict correct targets reliably. In short, LASSO regression helps to obtain sparse solution whenever possible. Use have used popular coordinate descent algorithm to minimize the convex loss function of LASSO. The github link for this project can be found
[here](https://github.com/mattsinbot/Coordinate-Descent-LASSO).

### Support Vector Machines Primal and Dual Solution
This project is associated to binary classification problem using SVM with Quadratic Programming as optimization algorithm. We solve the classification problem in two different ways, first by optimizing the primal formulation of SVM and secondly by solving the dual formulation of SVM. We checked whether both ways provide same solution to validate correctness of the implementation. We also tried to understand how to select a good threshold to find support vectors from the solution provided by quadratic programming. You can find the codes for this project [here](https://github.com/mattsinbot/SVM-Primal-Dual).
![SVM_basic](/images/ml/SVM-primal-Dual.png)

### Hard Negative Mining with SVM for Human Upper Body Recognition
Here we use SVM to detect human upper bodies in TV series The Big Bang Theory. To train such a classifier with SVM we need a set of images with bounding boxes of the upper bodies (data). Positive training data are image patches extracted at the annotated locations whereas negative training data are any image patch that does not significantly overlap with the annotated upper bodies. Thus number of negative training examples are many more than that of positive examples. However it is not possible to use all negative examples at a time because of memory limitation. To counter this problem we can use hard negative mining to find hardest negative examples and iteratively train an SVM. Expected output of this project is, given an image detect upper human bodies with a rectangular box with scores mentioned at the top-left. You can find the codes written to accomplish this project [here](https://github.com/mattsinbot/SVM-Upper-Body-Detection).
![SVM_hardneg](/images/ml/svm_hard_neg_minig.png)

### Stochastic Gradient Descent to Train Multiclass SVM
Look in the repository [here](https://github.com/mattsinbot/SVM-SGD-Multiclass).


### Train a GAN for Activity Recognition
Look into the *.ipynb* file [here](https://github.com/mattsinbot/Train-GAN-Activity-Recognition).

### Train a SVM to Find Phone
The task description, solution manual and codes can be found [here](https://github.com/mattsinbot/Find-Phone-SVM).

### Neural Network to Classify Iris Dataset
In this project we want to classify different species of Iris flowers from Iris-dataset. This data-set is highly nonlinear and hence can not be classified with linear classifier. We have introduced a three layer (1 input+ 1 hidden + 1 output) neural net which are fully connected to build the classifier. We have developed the model using PyTorch's `torch.nn` module. Our model was able to predict correct labels with 99% accuracy on test data. We have also computed *confusion* matrix to better visualize the prediction pattern of the model. The github link for this project can be found [here](https://github.com/mattsinbot/PyTorch-for-Iris-Dataset).

### Training DNN using PyTorch for Digit Recognition
In this project we show with MNIST data set of hand written digits, how to load data in PyTorch, how to do forward pass and backpropagation and finally training a deep-neural-network to recognize hand written digits.
We will again use PyTorch's `torch.nn` module to build and train the DNN. Once the network is trained, given the image of a hand-written digit as input, the trained model will be able to predict the right digit with high probability value. More details about this project can be found in the Jupyter notebook [here](https://github.com/mattsinbot/Pytorch-ML).
![digit_predict](/images/ml/digit_predict.png).
