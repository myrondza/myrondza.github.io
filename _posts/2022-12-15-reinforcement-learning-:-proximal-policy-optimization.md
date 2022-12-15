---
date: 2022-12-15 14:26:38
layout: post
title: "Reinforcement Learning : Proximal Policy Optimization"
subtitle:
description:
image: https://imgs.search.brave.com/PJ7FqZe7nnMD3BBlPpsM8j3bQIXa1keMO895MdYR048/rs:fit:1200:1200:1/g:ce/aHR0cHM6Ly9zdGF0/aWMwMS5ueXQuY29t/L2ltYWdlcy8yMDE5/LzEwLzE1L2F1dG9z/c2VsbC8xNXJ1Ymlr/c3JvYm90LXByb21v/LzE1cnViaWtzcm9i/b3QtcHJvbW8tdGhy/ZWVCeVR3b0xhcmdl/QXQyWC5qcGc
optimized_image:
category:
tags:
author:
paginate: false
---

## PPO

With supervised learning, we can easily implement the cost function, run gradient descent on it, and be very confident that we’ll get excellent results with relatively little hyperparameter tuning. The route to success in reinforcement learning isn’t as obvious — the algorithms have many moving parts that are hard to debug, and they require substantial effort in tuning in order to get good results. PPO strikes a balance between ease of implementation, sample complexity, and ease of tuning, trying to compute an update at each step that minimizes the cost function while ensuring the deviation from the previous policy is relatively small.

We’ve [previously](https://channel9.msdn.com/Events/Neural-Information-Processing-Systems-Conference/Neural-Information-Processing-Systems-Conference-NIPS-2016/Deep-Reinforcement-Learning-Through-Policy-Optimization) detailed a variant of PPO that uses an adaptive [KL](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence) penalty to control the change of the policy at each iteration. The new variant uses a novel objective function not typically found in other algorithms:

### Clipped Surrogate Objective

TRPO maximizes a “surrogate” objective


CPI is the conservative policy iteration

Without a constraint, `maximization` of L
CPI would lead to an `excessively large policy`
update; hence, we now consider how to modify the objective, to `penalize` changes to the policy that move `rt(θ)` away from 1.

The main objective proposed is the following:

$$
LCLIP(θ)=E^t[min(rt(θ)A^t,clip(rt(θ),1−ε,1+ε)A^t) ] 
$$

- `θ` is the policy parameter
- *`E*^*t*` denotes the empirical expectation over timesteps
- *`rt*` is the ratio of the probability under the new and old policies, respectively
- *`A*^*t`* is the estimated advantage at time *t*
- `ε` is a hyperparameter, usually 0.1 or 0.2

The motivation for this objective is as follows. 

The first term inside the min is `LCPI` . 

The second term, `clip(rt(θ), 1−, 1+)Aˆt,` modifies the surrogate
objective by `clipping the probability ratio` 

which removes the incentive for moving `rt` outside of the interval [1 − , 1 + ].

Finally, we take the minimum of the clipped and unclipped objective, so the
final objective is a lower bound (i.e., a pessimistic bound) on the unclipped objective.

L CLIP (θ) = L CPI (θ) to first order around `θold` (i.e., where r = 1), however, they become different as `θ` moves away from `θold`.

This objective implements a way to do a Trust Region update which is compatible with Stochastic Gradient Descent, and simplifies the algorithm by removing the KL penalty and need to make adaptive updates. In tests, this algorithm has displayed the best performance on continuous control tasks and almost matches ACER’s performance on Atari, despite being far simpler to implement.

### Adaptive KL Penalty Coefficient

Another approach, which can be used as an alternative to the clipped surrogate objective, or in addition to it, is to use a `penalty on KL divergence`, and to adapt the penalty coefficient so that we achieve some target value of the KL divergence d targ each policy update.

PPO Algorithm

The `surrogate losses` from the previous sections can be computed and differentiated with a minor change to a typical policy gradient implementation. For implementations that use automatic differentation, one simply constructs the loss 

L CLIP or L KLPEN instead of L PG, and one performs
`multiple steps of stochastic gradient ascent` on this objective

Most techniques for computing variance-reduced advantage-function estimators make use a learned state-value function V (s)

This objective can further be augmented by adding an entropy bonus to ensure sufficient exploration

In the case where the globally optimal behaviour is difficult to learn due to sparse rewards or other factors, an agent can be forgiven for settling on something simpler, but less optimal. 

Entropy bonuses are used because without them an agent can too quickly converge on a policy that is locally optimal, but not necessarily globally optimal

The entropy bonus is `used to attempt to counteract this tendency by adding an entropy increasing term to the loss function`



where `c1`, `c2` are coefficients, and `S` denotes an entropy bonus, and L V Ft is a squared-error loss

At a high level, the PPO algorithm works by first choosing an action based on the current state of the environment. The AI then receives a reward based on how good or bad the chosen action was. The PPO algorithm then uses this information to adjust the AI's decision-making process, so that it will be more likely to choose good actions in the future. This process is repeated many times, allowing the AI to continually improve its ability to take the best possible actions in the given environment. Yes yeah