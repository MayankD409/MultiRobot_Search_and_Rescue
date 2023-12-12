# Swarm Robot Search & Rescue

[![codecov](https://codecov.io/gh/lorocks/Swarm_Robot_Search_and_Rescue/graph/badge.svg?token=EN89MI8GLH)](https://codecov.io/gh/lorocks/Swarm_Robot_Search_and_Rescue)

![CICD Workflow status](https://github.com//lorocks/Swarm_Robot_Search_and_Rescue/actions/workflows/run-unit-test-and-upload-codecov.yml/badge.svg)

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

# Overview
This repository consists of a Swarm Robotic implementation for Search and Rescue (SaR) operations

## Authors
 - Lowell Lobo: Graduate Student in Enginnering, Robotics in University of Maryland
 - Mayank Deshpande: Graduate Student in Enginnering, Robotics in University of Maryland

## Purpose 
Acme requires a 5-year R&D product roadmap for multi-agent or swarm robotics implementations. The research topic chosen is search and rescue operations using multi-agent robots. SaR operations are often challenging and hazardous, requiring personnel to navigate complex environments and locate individuals or objects in distress. Traditional SAR methods rely heavily on human operators, which can be time-consuming, resource-intensive, and potentially dangerous. The use of robotic systems offers a promising alternative, providing enhanced capabilities and reducing the risks associated with SAR missions

## Assumption
The map of the area is provided in advance for the robots to navigate through. 
The object that needs to be found is stationary and not in motion.

## Features
 - C++ API for autonomous navigation around map by all the robots and object detection
 - GitHub Repository with CI and CodeCov
 - UML and Dependency Diagrams
 - Doxygen Documentation

## Constraints
Simulating a large number of robots within a restrictive space and ensuring no collisions while considering optimal autonomous path planning is a challenging task. The runtime fps and memory management depend on the physical constraints of each system. Latency in terms of communication between all 20+ robots depends on the robot hardware as well as environmental factors. Bad weather or remote locations can lead to bad communication.

# Process
The project will follow AIP concepts and be performed using Pair Programming. After a specific time frame, driver and navigator roles will be swapped. 
The module work such that the Gazebo environment is setup with the Gazebo world, area map and robots spawned. The robots will then move through the map, while consequently searching for objects of interest. The process is repeated until the object is found. Once the object is found, the corresponding robot who located the object will ping he location of the object.
Testing of components is performed using GoogleTest, and system testing will be performed every iteration for overall functionality verification. Furthermore, Level 2 integration tests will be performed to evaluate performance of nodes in the global level.

# AIP Methodology
The project will take two weeks to complete over two iterations, consisting of Phase-1 and Phase-2, where each iteration is for one week. Since the project consists of only two members, only product backlog, daily meetings and iteration meetings in the AIP model will be performed. Project monitoring will be done using timely git commits, and the navigator ensures code quality. Daily meetings will be held for error correction based on code coverage and GitHub CI reports.

# Links
## Video Links

## AIP Document Links
[AIP Google Sheet](https://docs.google.com/spreadsheets/d/1iOmKEHb6u9iLjWMfp7kFqTMgQoor1WnGJIepN5Y3yEI/edit#gid=0)

[Sprint Notes](https://docs.google.com/document/d/1D7xS4Swq-WIUK4QaRhk47Q6qZ8-QHxehfrI1YFuxjTo/edit)

# Dependencies
The project will be built in a ROS2 environment for simulation, but the module will be built in C++ using CMake build tools running on Ubuntu 22.04. OpenCV, an open-source licensed Apache2 library will be used in the implementation. ROS2 is licensed under Apache2.0 License and is a widely used framework for robotic applications. Turtlebot3 has an Apache2.0 License and is the package used to simulate the Turtlebot3 in Gazebo.
Algorithms that employ HSV manipulation of images using OpenCV will used for object detection, and GitHub will be used for version control, code coverage reports and running unit tests.

# Development
## Packages
 - sar: A C++ API used for navigation and object detection with robotd
 - multi_robot: A package created to use the sar API for Search & Rescue operations and Swarm implementation

## Phase 1
For Phase 1, the initial design of UML diagrams and empty implementation with class stubs and placeholder unit tests are created.


# Build Commands
## How to generate package dependency graph

``` bash
colcon graph --dot | dot -Tpng -o depGraph.png
open depGraph.png
```
[<img src=screenshots/depGraph.png
    width="20%" 
    style="display: block; margin: 0 auto"
    />](screenshots/depGraph.png)



## How to build

```bash
rm -rf build/ install/
colcon build 
source install/setup.bash
```

## How to build for tests (unit test and integration test)

```bash
rm -rf build/ install/
colcon build --cmake-args -DCOVERAGE=1 
```

## How to run tests (unit and integration)

```bash
source install/setup.bash
colcon test
# View test results
colcon test-result --all --verbose
```

## How to generate coverage reports after running colcon test

First make sure we have run the unit test already.

```bash
colcon test
```

### Test coverage report for `multi_robot`:

``` bash
ros2 run multi_robot generate_coverage_report.bash
open build/multi_robot/test_coverage/index.html
```

### Test coverage report for `sar`:

``` bash
colcon build \
       --event-handlers console_cohesion+ \
       --packages-select sar \
       --cmake-target "test_coverage" \
       --cmake-arg -DUNIT_TEST_ALREADY_RAN=1
open build/sar/test_coverage/index.html
```

### combined test coverage report

``` bash
./do-tests.bash
```

## How to generate project documentation
``` bash
./do-docs.bash
```

