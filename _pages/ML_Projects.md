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
![SVM_basic](/images/ml/SVM-primal-Dual.png)

This project is associated to binary classification problem using SVM with Quadratic Programming as optimization algorithm. We solve the classification problem in two different ways, first by optimizing the primal formulation of SVM and secondly by solving the dual formulation of SVM. We checked whether both ways provide same solution to validate correctness of the implementation. We also tried to understand how to select a good threshold to find support vectors from the solution provided by quadratic programming. You can find the codes for this project [here](https://github.com/mattsinbot/SVM-Primal-Dual).


### Hard Negative Mining with SVM for Human Upper Body Recognition
![SVM_hardneg](/images/ml/svm_hard_neg_minig.png)

Here we use SVM to detect human upper bodies in TV series The Big Bang Theory. To train such a classifier with SVM we need a set of images with bounding boxes of the upper bodies (data). Positive training data are image patches extracted at the annotated locations whereas negative training data are any image patch that does not significantly overlap with the annotated upper bodies. Thus number of negative training examples are many more than that of positive examples. However it is not possible to use all negative examples at a time because of memory limitation. To counter this problem we can use hard negative mining to find hardest negative examples and iteratively train an SVM. Expected output of this project is, given an image detect upper human bodies with a rectangular box with scores mentioned at the top-left. You can find the codes written to accomplish this project [here](https://github.com/mattsinbot/SVM-Upper-Body-Detection).

### Stochastic Gradient Descent to Train Multiclass SVM
Look in the repository [here](https://github.com/mattsinbot/SVM-SGD-Multiclass).


### Train a GAN for Activity Recognition
Look into the *.ipynb* file [here](https://github.com/mattsinbot/Train-GAN-Activity-Recognition).

### Train a SVM to Find Phone
The task description, solution manual and codes can be found [here](https://github.com/mattsinbot/Find-Phone-SVM).

### Neural Network to Classify Iris Dataset
In this project we want to classify different species of Iris flowers from Iris-dataset. This data-set is highly nonlinear and hence can not be classified with linear classifier. We have introduced a three layer (1 input+ 1 hidden + 1 output) neural net which are fully connected to build the classifier. We have developed the model using PyTorch's `torch.nn` module. Our model was able to predict correct labels with 99% accuracy on test data. We have also computed *confusion* matrix to better visualize the prediction pattern of the model. The github link for this project can be found [here](https://github.com/mattsinbot/PyTorch-for-Iris-Dataset).

### Training DNN using PyTorch for Digit Recognition
![digit_predict](/images/ml/digit_predict.png).

In this project we show with MNIST data set of hand written digits, how to load data in PyTorch, how to do forward pass and backpropagation and finally training a deep-neural-network to recognize hand written digits.
We will again use PyTorch's `torch.nn` module to build and train the DNN. Once the network is trained, given the image of a hand-written digit as input, the trained model will be able to predict the right digit with high probability value. More details about this project can be found in the Jupyter notebook [here](https://github.com/mattsinbot/Pytorch-ML).

### Design of Neuro-Observer of Robots
In this project we synthesized a nonlinear system-state-observer for two single-input-single-output
nonlinear systems. We use neural network to capture nonlinearity of the observer. No linearity
with respect to the unknown system parameters is required for the designed observer. The observer
stability and boundedness of the state estimates and NN weights are proven. In order to show the
effectiveness of the proposed observer, two simulations are carried out. First we modeled NN based
observer for a single-link robot, rotating in vertical plane with two sets of example data sets to train the NN embeded into the observer. The second observer is designed for Van der Pol oscillator. For the single-link observer, tests are performed with no-noise training data set and with noisy dataset as well. It has been observed that NN based observer learned more accurately and faster from the no-noise data set as compared to noisy data set which leads to longer learning time. The GitHub link for this project's codes and full documentation report can be found [here](https://github.com/mattsinbot/Neuro-Observer-for-Dynamical-Systems).

### EKF-for-Trajectory-Estimation
The project focuses on the control of a mobile robot that intends to go from a given initial position to a desired goal position. The robot has to generate a path from initial to final position while avoiding obstacles simultaneously. The robot here is considered as a point mass robot.

![evol_cost](/images/control/Value_growth9.gif)

**Evolution of cost in Value-Iteration**

![exp_op](/images/control//Obs_Avoidance196.gif)

**Figure above shows, how a robot uses partially observable states to reach from start to goal while avoiding the obstacles**


1. Generated mesh grid and put obstacles in the grid
2. Use Dynamic Programing to figure out the path that avoids obstacles while simultaneously moving from initial to goal
3. Test the algorithm with different buffer size around the obstacles
4. Smoothing the way-points in the path
5. Generating trajectory that follows uniform speed of 1.5 through out the path
6. Designing a Control-Law considering Actuator-Constraints while tracking the desired trajectory
7. Designing an Observer by Reduced-Order-Observer method
8. Implementing Separation-Principle to combine Controller and Observer

### Machine Learning Lecture Notes
The repository can be found [here](https://github.com/mattsinbot/Lecture-Slides).
