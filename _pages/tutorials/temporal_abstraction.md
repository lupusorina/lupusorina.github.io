---
layout: default
title: "Temporal Abstraction"
permalink: /tutorials/temporal_abstraction/
---

# Temporal Abstraction

*Temporal abstraction* is the ability to reason or make decisions over extended time intervals by grouping sequences of actions or events into higher-level units (e.g., "open the door" instead of "step forward, turn left, step forward"). It allows planning and learning at multiple time scales.

## Options

One solution is to use *options*, introduced in [[1]](#references), to represent the high-level actions.
"An option consists of 1. an option policy that directs the agent's behavior for a subset of the environment states, 2. an initiation set consisting of all the states in which the option can be initiated and 3. a termination condition which specified the conditions under which the option terminates.
It is important to note that an option is not a sequence of actions; it is a **closed-loop control** rule, meaning that it is responsive to on-going state changes" [2].

### Example: Torque-limited Inverted Pendulum
One example we can think of is the control of a *torque-limited* inverted pendulum.
To swing up this pendulum, we need two tracking controllers: 
a) a swing-up controller: usually based on energy shaping control 

$$u = - k \dot{\theta} \tilde{E},$$

where $$k$$ is the gain, $$\tilde{E}$$ is the energy error, and $$\dot{\theta}$$ is the angular velocity,
and b) a balancing controller: usually based on LQR or nonlinear stabilizing controller, such as

$$u = - K_p \theta - K_d \dot{\theta},$$

where $$K_p$$ and $$K_d$$ are the proportional and derivative gains, respectively.

Let's consider swinging up of this system in the *options* framework:

*Option 1: "Swing up"*
- Initiation set: All downward positions or low-energy states.
- Policy: Energy-shaping control to increase the total energy toward upright.
- Termination: When the pendulum is close enough to the upright region.

*Option 2: "Balance"*
- Initiation set: Small region around the upright position.
- Policy: LQR or nonlinear stabilizing controller.
- Termination: Never (or when falling out of the upright region).

## Semi-MDPs

MDPs are not able to represent the temporal abstraction because they are defined over a single time step.
Instead, semi-MDPs are a generalization of MDPs.

In semi-Markov options, the policy and termination condition are functions of possible histories, such as 
$$
\pi : \Sigma \times \mathcal{A} \to [0, 1],
$$ and the termination condition is $$\beta : \Sigma \to [0, 1]$$.





## References

[1] R. S. Sutton, D. Precup, S. Singh, ``Between MDPs and Semi-MDPs: A Framework for Temporal Abstraction in Reinforcement Learning,'' 1998.

[2] S. Singh, A. Barto, N. Chentanez,``Intrinsically Motivated Reinforcement Learning,'' 2004.