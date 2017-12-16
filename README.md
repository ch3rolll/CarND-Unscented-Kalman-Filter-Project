# Unscented Kalman Filter Project Starter Code
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= v3.5
* make >= v4.1
* gcc/g++ >= v5.4

## Basic Build Instructions

1. mkdir build
2. cd build
3. cmake ..
4. make
5. ./UnscentedKF


## Initialization paramaters
Since the instruction suggestes to tune `std_a`, `std_yawd`

* `std_a_`: process noise standard deviation longitudinal acceleration in m/s^2. I picked up a value of 2 here

* `std_yawd_`: process noise standard deviation yaw acceleration in rad/s^2. A big would have to swerve pretty heavily for a big acceleration in yaw, so I settled for .5 radians here.
* Radar
  * `x_`: Most of this is just an equation for the state space based off the first radar measurement. The middle value, for 'v', can be tuned. I set this to a value of 4 m/s as a quick Google search led me to an average bike speed of 15.5 km/h, which is just over 4 m/s
  * `P_`: The diagonal of the matrix are the variances for each value within the `x_` state space (px, py, v, yaw, yawd). Radar feeds in rho, phi and rhodot. We are given the standard deviation of each of these, and the square of the standard deviation is the variance. Although this is not the exact right value (given its in a different state space), I used the square of the given standard deviations to calculate reasonable values for `P_` (other than for the middle value of 'v' which I just set to 1.
* Lidar
  * `x_`: The first two values are filled by the 'px' and 'py' lidar measurements. I chose 4 m/s for 'v' in the same way as for radar. I chose yaw of .5 as a reasonable estimate of a beginning turn, with yawd as 0 given no expected big swerves at the start.
  * `P_`: We are given the standard deviations for px and py from the lidar measurements, so I squared these to feed in the respective variances to the matrix. I just used 1 for the other variances along the diagonal as a reasonable beginning value.

## Results
Based on the provided data set, my Unscented Kalman Filter will produce the below results. The x-position is shown as 'px', y-position as 'py', velocity in the x-direction is 'vx', while velocity in the y-direction is 'vy'. Residual error is calculated by mean squared error (MSE).

| Input |   MSE   |
| ----- | ------- |
|  px   | 0.06908 |
|  py   | 0.07967 |
|  vx   | 0.16735 |
|  vy   | 0.20016 |

---

