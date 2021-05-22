# PID Controller

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

Fellow students have put together a guide to Windows set-up for the project [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/files/Kidnapped_Vehicle_Windows_Setup.pdf) if the environment you have set up for the Sensor Fusion projects does not work for this project. There's also an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3).

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

## Reflection

Describe the effect each of the P, I, D components had in your implementations.   
What you expected? Through P component, I expected the control valve moved quickly when I increased P value. This helps to access the setpoint as the value is increased. However P component cannot converge a stable value. Regarding I component, through the experiments, I component make the stability to be weak because of making a large signal. Therefore, I set it to zero not to use it. Through D component, I expected the overshoot was suppressed when I increased D value.   
Here is some examples to show which is considered.   
In case of P = 0.5, I = 0.0, D = 0.0   
Link: ./video/only_P_component.m4v   

In case of P = 0.2, I = 0.0, D = 5.0   
Link: ./video/P_and_D_components.m4v   

Therefore, finally I chose the set (P = 0.2, I = 0.0, D = 5.0)

How I chose the final hyperparameters. First of all, I tried to find manually. Here is the list for my core try-outs.   
| Try-out No. |   P   |   I   |   D   |                        Remark                      |
|-------------|-------|-------|-------|----------------------------------------------------|
|      01     |   0   |   0   |   0   |                     Initial try-out                |
|      02     |  0.5  |   0   |   0   |                   I give a value of P.             |
|      03     |  0.2  |   0   |  0.5  |  For stability, I give D value and reduce P value. |
|      04     |  0.1  |  0.1  |  0.8  |  I try to give I value to help find optimal value. |
|      05     |  0.1  | 0.001 |  0.9  |  I value cannot help to control much in this env.  |
|      06     |  0.2  |   0   |  0.9  |  To overcome the rapid curve, I increase P value.  |
|      07     |  0.2  |   0   |  5.0  |  Finally, to be stable, I increase D value more.   |   
