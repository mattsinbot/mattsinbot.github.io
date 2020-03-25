---
title: "Control Project"
permalink: /controlsprojects/
header:
  image: "/images/control/control_profile_picture.png"
---


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
