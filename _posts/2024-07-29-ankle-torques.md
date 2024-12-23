---
layout: post
title:  ankle actuators
date:   2024-07-29 13:39:00
description: How to design ankles that are actuated
tags: robotics biped
---

 I initially designed the robot without actuated ankles, planning to add ankle torques once the robot achieved walking.
However, the initial design required the robot to step quickly, making testing by myself extremely challenging.
Now, it's time to invest in designing the actuated ankles.

--------------

### Design

I consider three options:

1. **motor + low gear ratio (cable-driven)**
<br> 👍: It is a compact design
<br> 👎:  Less experience designing this. The cable needs to not stretch over time.
2. **motor + low gear ratio (belt-driven)**
<br> 👍: experience designing belt-driven actuators, as I've already designed some for the knee and yaw joints.
<br> 👎: It might be too bulky/heavy
3. **series elastic actuators**
<br>  👍: Can absorb impacts better
<br>  👎: Less experience designing this. I need to find a way to measure the spring deflection.

--------------

### Controls

For the control, I would like to employ a straightforward feedback law. I'm not trying at this point to do something very complicated, because I want to get the robot to walk first.
So I want something along the lines of 
$$
u = - k_p x_{zmp} - k_d v,
$$
 where zmp stands for zero moment point.
 Initially, I was thinking to use the velocity of the zmp. However, I believe that signal will be too noisy.
So I can use the ankle velocity computed geometrically as the robot moves forward. 

--------------


I decided to go with the series elastic actuators, so I'll document the sizing, manufacturing, and testing in a separate blog post.






