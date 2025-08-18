---
layout: default
title: "Time Discretization in RL"
permalink: /tutorials/time_discretization/
---

Let's talk about time discretizations in RL, specifically in the context of rewards. To write this summary, I got inspired by the paper "An Idiosyncrasy of Time-discretization in Reinforcement Learning" by [Kris de Asis](https://kris.pengy.ca) and [Richard S. Sutton](http://incompleteideas.net) and by all the inconsistencies I see in many of the RL papers, especially empirical ones.


Time discretization is a key consideration when implementing reinforcement learning algorithms on a robot. Most robotic systems operate in discrete time, with control inputs applied at fixed frequencies. 

Let the undiscounted return from the start state in continuous time be

$$
G_0 = \int_0^T r(t) dt,
$$

where $$r(t)$$ is the reward function and $$T$$ is the time horizon, and $$dt$$ is the time step.
In literature, people use the discounted return, which just adds a discount factor to the integral, as follows

$$
\int_0^T \gamma^t r(t) dt.
$$

where $$\gamma$$ is the discount factor between $$[0, 1)$$.
An alternative is to use an exponential discount factor, which is more common if you come from a controls background. I find this perspective more intuitive, as the exponential form defines a natural time constant, the horizon over which future rewards contribute, rather than relying on a unitless multiplicative factor per step. The latter is more common with financial and economics literature.

$$
\int_0^T e^{-\gamma_c t} r(t) dt.
$$


Let's transform this integral in discrete time (using the Riemann sums), as follows

$$
\sum_{k=1}^{N} e^{-\gamma_c k \Delta t} r(k \Delta t) \Delta t,
$$

where $$N = \frac{T}{\Delta t}$$.
Using the notation of $$\gamma_d = e^{-\gamma_c \Delta t}$$, we can rewrite the sum as

$$
\sum_{k=1}^{N} \gamma_d^k r(k \Delta t) \Delta t,
$$

where $$\gamma_d$$ is the discrete discount factor.

In practice most RL papers just treat the discrete discount factor $$\gamma_d$$ as a hyperparam between $$[0, 1)$$. But if you think in continuous time, there's a clean way to interpret it and compute the corresponding discrete $$\gamma_d$$. In fact, $$\gamma_c$$ has units of $$1/time$$, so it sets a natural timescale. 
This way, your algorithm is invariant to the discretization, rather than treating $$\gamma_d$$ as a random tuning knob, like in every other RL paper.

Ok, so how would you think about it? A good start is to say: after $$H$$ steps, future rewards contribute less than $$10\%$$ of their original weight. Let $$\epsilon=0.1$$, then

$$
e^{-\gamma_c H} = \epsilon,
$$

or

$$
\ln e^{-\gamma_c H} = \ln(\epsilon),
$$

with the final result being

$$
H = \frac{\ln(\frac{1}{\epsilon})}{\gamma_c}.
$$

So for $$\gamma_c = 0.1 s^{-1}$$, we get a horizon of $$H = 23$$ seconds.

Let's compute $$\gamma_d$$, which is

$$
\gamma_d = e^{-\gamma_c \Delta t},
$$

so for a $$\Delta T=0.05 s$$ or a rate of $$20 Hz$$, we have

$$
\gamma_d = e^{-0.1 \times 0.05} = 0.995.
$$

Note that for episodic RL, the episode ends at a fixed time $$T$$. If the effective horizon $$H$$ is shorter than the episode length, then discounting is what really controls how far ahead the agent plans. If the episode length is shorter than the effective horizon, then the episode cutoff dominates.

Here's the summary:

- $$\gamma_d$$ depends explicitly on $$\Delta t$$. 
- If you change the simulation/control frequency (e.g., from 10 Hz to 100 Hz), the same $$\gamma_d$$ no longer means the same planning horizon.
- What's invariant is $$\gamma_c$$, because it has physical units ( $$1 /$$ time ).
- Best practice: think in continuous time first, then compute $$\gamma_d$$.
- Don't forget to multiply the reward by $$\Delta t$$.


## Acknowledgments
To [Kris de Asis](https://kris.pengy.ca) for feedback and corrections on the blog post.