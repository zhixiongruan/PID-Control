# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## PID-Controls

### P代表着比例项，D代表着微分项，I代表着积分项

**P (Proportional)**
这个分量使汽车的转向角度与横切误差（CTE）成比例。这意味着误差越大，朝着参考航线会有一个更大的转向角度，随着接近参考航线，转向角度也会渐渐变小，最终会挨到参考航线。如果只使用 P 一项，汽车会在参考航线附近反复越界，永远无法收敛，即车辆在道路上振荡。P 分量系数（Kp）的值越大，震荡得更快。

**D (Differential)**
这个分量的引入是为了避免越界和过冲，它与CTE随时间的导数成正比。适当调整的D参数将使汽车平稳地接近中心线，另外较高的P值也需要较高的D值。

**I (Integral)**
为了抵消系统的偏差而引入了积分项I，CTE积分也就是历史观察到的所有CTE的和。在不存在系统偏差的理想情况下，则不需要使用该分量。

### 超参数值选择

我手动调整了3个分量的系数，首先我分别设置了一项为 1.0，其它为 0.0 的情况，三种情况分别是：
 * [Kp=1.0,Ki=0.0,Kd=0.0](./videos/P.mp4)
 * [Kp=0.0,Ki=1.0,Kd=0.0](./videos/I.mp4)
 * [Kp=0.0,Ki=0.0,Kd=1.0](./videos/D.mp4)
 
然后我参照课程里的参数设置，从Kp=0.2，Ki=0.004，Kd=3.0开始调整。因为模拟器是比较理想的环境，所以我设置 Ki=0.0，然后依次再调整Kp和Kd，最终选定
Kp=0.15，Ki=0.0，Kd=2.0，最后效果参见视频 [PID.mp4](./videos/PID.mp4)。

### 改进及学习

对Twiddle的使用效果不理想，还需要加强掌握。

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

