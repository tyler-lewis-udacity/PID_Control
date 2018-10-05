# P.I.D. Control
Self-Driving Car Engineer Nanodegree Program

---

## Project Description
The goal of this project was to implement a PID controller in C++ 
capable of maneuvering a vehicle around a track.  The simulator used 
for this project was provided by Udacity.  Cross track error (CTE) and vehicle speed data are sent from the simulator to the PID controller.  The data is then used to calculate the required vehicle steering angle.


## Reflection

 - Describe the effect each of the P, I, D components had in your implementation:

##### Proportional (P) Component
The proportional component of the controller adjusts the steering angle in direct proportion to the cross track error.  For example, if the car is slightly too far the left of the desired path, the steering angle will be turned slightly to the right to correct this error.  If the car is very far to the left of the desired path, the steering angle will be turned a large amount to the right to correct for this error.  

The proportional controller does better than simple "bang-bang" steering, but using a proportiona controller alone results in the car repeatedly overshooting the desired path causing constant oscillation.  

##### Derivative (D) Component
The derivative component of the controller adjusts the steering angle based on the cross track error rate (CTER).  The CTER measures how quickly the vehicle is approaching the desired path.  The derivative component counters the overshoot problem of the proportional component by attempting to minimise the CTER. If the derivative component is too low, the vehicle oscilations occur as they would in a proportional-only controller.  If the derivative component is set too high, the vehicle is not able to alter its course quicly enough and under-steers around corners.

Together the proportional and derivative components form a decent controller.  However, over time a steady state error can accumulate.

##### Integral (I) Component
The integral component of the PID controller provides subtle correction to the steering angle to combat steady state error.  Over long periods of time, the steady state error slowly builds.  Neither the proportional or derivative components can counter this error, so the integral term is added to form the complete controller.


 - Describe how the final hyperparameters were chosen:

The gain, or "strength", of each of the three components described above need to be tuned in order for the controller to behave properly.  The gains for this project were tuned manually using the general procedure found [here](https://robotics.stackexchange.com/questions/167/what-are-good-strategies-for-tuning-pid-loops){:target="_blank"}.

The final gains selected were: 

 - Kp = 0.4
 - Kd = 5.0
 - Ki = 0.00001

 The gains allow the car to travel around the track relatively well.  However, better results could probably be achieved using a tuning algorithm such as the "Twiddle" algorithm covered in the lessons.  


---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.

## Hints!

* You don't have to follow this directory structure, but if you do, your work
  will span all of the .cpp files here. Keep an eye out for TODOs.

## Call for IDE Profiles Pull Requests

Help your fellow students!

We decided to create Makefiles with cmake to keep this project as platform
agnostic as possible. Similarly, we omitted IDE profiles in order to we ensure
that students don't feel pressured to use one IDE or another.

However! I'd love to help people get up and running with their IDEs of choice.
If you've created a profile for an IDE that you think other students would
appreciate, we'd love to have you add the requisite profile files and
instructions to ide_profiles/. For example if you wanted to add a VS Code
profile, you'd add:

* /ide_profiles/vscode/.vscode
* /ide_profiles/vscode/README.md

The README should explain what the profile does, how to take advantage of it,
and how to install it.

Frankly, I've never been involved in a project with multiple IDE profiles
before. I believe the best way to handle this would be to keep them out of the
repo root to avoid clutter. My expectation is that most profiles will include
instructions to copy files to a new location to get picked up by the IDE, but
that's just a guess.

One last note here: regardless of the IDE used, every submitted project must
still be compilable with cmake and make./

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).

