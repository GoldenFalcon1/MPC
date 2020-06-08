# MPC
## Project Description

### Overview

**Model predictive control (MPC)** is an advanced method of process control which relies on dynamic models of the process.
Differently from previously implemented. MPC controller has the ability to anticipate future events and can take control actions accordingly. Indeed, future time steps are taking into account while optimizing current time slot.

The MPC controller framework consists in four main components:
 - **Trajectory** taken in consideration during optimization. This is parametrized by a number of time steps ***N*** spaced out by a time ***dt***. Clearly, the number of variables optimized is directly proportional to *N*, so this must be considered in case there are computational constraints.
 
 - **Vehicle Model**, which is the set of equations that describes system behavior and updates across time steps. In our case, we used a simplified kinematic model (so called *bycicle model*) described by a state of six parameters:
   - **x** car position (*x-axis*)
   - **y** car position (*y-axis*)
   - **psi** car's heading direction
   - **v** car's velocity
   - **cte** cross-track error
   - **epsi** orientation error
   
  
 - **Contraints** necessary to model contrants in actuators' respose. For instance, a vehicle will never be able to steer 90 deegrees in a single time step. In this project we set these constraints as follows:
   - **steering**: bounded in range [-25°, 25°]
   - **acceleration**: bounded in range [-1, 1] from full brake to full throttle
   
 - **Cost Function** on whose optimization is based the whole control process. Usually cost function is made of the sum of different terms. Besides the main terms that depends on reference values (*e.g.* cross-track or heading error), other regularization terms are present to enforce the smoothness in the controller response (*e.g.* avoid abrupt steering).
 
  
   
### Tuning Trajectory Parameters

Both ***N*** and ***dt*** are fundamental parameters in the optimization process. In particular, ***T = N * dt*** constitutes the *prediction horizon* considered during optimization. These values have to be tuned keeping in mind a couple of things:
  - large *dt* result in less frequent actuations, which in turn could result in the difficulty in following a continuous reference trajectory (so called *discretization error*) 
  - despite the fact that having a large *T* could benefit the control process, consider that predicting too far in the future does not make sense in real-world scenarios.
  - large *T* and small *dt* lead to large *N*. As mentioned above, the number of variables optimized is directly proportional to *N*, so will lead to an higher computational cost.



## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!
