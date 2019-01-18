# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program

## Goals
In this project your goal is to safely navigate around a virtual highway with other traffic that is driving +-10 MPH of the 50 MPH speed limit. You will be provided the car's localization and sensor fusion data, there is also a sparse map list of waypoints around the highway. The car should try to go as close as possible to the 50 MPH speed limit, which means passing slower traffic when possible, note that other cars will try to change lanes too. The car should avoid hitting other cars at all cost as well as driving inside of the marked road lanes at all times, unless going from one lane to another. The car should be able to make one complete loop around the 6946m highway. Since the car is trying to go 50 MPH, it should take a little over 5 minutes to complete 1 loop. Also the car should not experience total acceleration over 10 m/s^2 and jerk that is greater than 10 m/s^3.

## Project rubrics

### Compilation

The code compiles correctly and without any warning.

### Valid Trajectories

The car was able to drive at least 4.32 miles without incident (tested several times and up to 10 miles). It drives according to the speed limit of 50 MPH (its reference maximum velocity is set to 49.5 MPH). Maximum acceleration and jerk were not exceeded, because reference velocity is increased and decreased with a small value only. There were no collisions with other cars. The car stayed in its lane, except for the time between changing lanes. The car is able to change lanes. If a car ahead is too close, it checks whether any other lane is possible and better to drive. If so, a lane change is issued.

### Reflection

The code model for generating paths is based on the Q&A walk-through video.

Sensor fusion data is used to predict positions of all other vehicles.

The behavioral part of the model checks for each lane if there is a car too close ahead (< 30 m) or behind (< 10 m). If there is a car too close ahead, velocity is decreased and a lane change is considered. A lane change occurs if the desired lane is free (no vehicle too close behind) and better (vehicles ahead more far away than on current lane). Otherwise the current lane is kept.

Trajectories are calculated according Q&A walk-through video. A path with several points is built up from car's current position, previous path's end point and points several ten meters ahead. Then a spline is calculated and the missing points of th previous path is filled up with new points. The distance of these points is calculated according to the desired reference velocity.

For mathematical simplicity, (x,y) coordinates are transferred from world's perspective to car's perspective and backwards in the end.