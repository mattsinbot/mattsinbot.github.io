---
title: "Software Engineering"
permalink: /dsalgprojects/
header:
---

### Multi-Threading-CPP
Visit the repository [here](https://github.com/mattsinbot/Multi-Threading-CPP).

![output_image](./images/software/Traffic_Signal.gif)

Traffic signal control for safe driving using C++. There are two rules to cross a junction by any vehicle (moving circles)
* wait unless the traffic signal associated to that junction is green.
* whoever comes first in the junction, gets the first entry into the junction (FIFO).

Each vehicle runs in a separate thread. Further, each junction (intersection) maintains a separate thread to keep track of the traffic-lights states (red/green) and how many vehicles are waiting to get into the junction. Whenever a vehicle enters into a junction, it randomly selects the next destination junction which are immediately connected to the current junction.

Please note, classes like **Vehicle**, **Intersection**, **TrafficeLight** and **Street** are all derived from the base class **TrafficObject**. More specifically, all these derived classes *override* the *simulate* method of the base class **TrafficObject**.

Further, the **Graphics** class is responsible for plotting the relevant objects at a frequency of **1 millisecond**. It uses **OpeCV** to plot the frames at the specified rate. The plotting mechanism is as following, (a) plot the map (background) as a static image first. Then overlay two transparent images one for the animating traffic-light and another for animating the vehicles.

I have compiled the project using C++11 standard linked with -pthread and -opencv in NetBeans IDE. The screen-shots for the build instructions in NetBeans IDE can be found in the folder named **build_setting_instructions**.


### Key Problems in Tree and Graph Traversal using C++
Visit the repository [here](https://github.com/mattsinbot/Problems-CPP).

### C++ Refresher
The repository can be found [here](https://github.com/mattsinbot/Refresher-CPP).

### Tests and Evaluations from various companies
The repository can be found [here](https://github.com/mattsinbot/Company-Technical-Evaluations).

### Udacity projects
The repository can be found [here](https://github.com/mattsinbot/DataStructures-Algorithms).

### Python Refresher
The repository can be found [here](https://github.com/mattsinbot/Refresher-Python).
