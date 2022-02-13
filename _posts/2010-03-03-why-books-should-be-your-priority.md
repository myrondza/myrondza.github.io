---
date: 2018-11-22 12:26:40
layout: post
title: Optimization Theory
subtitle: Lorem ipsum dolor sit amet, consectetur adipisicing elit.
description: Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
image: https://raw.githubusercontent.com/myrondza/myrondza.github.io/master/assets/img/Objective.png
optimized_image: https://raw.githubusercontent.com/myrondza/myrondza.github.io/master/assets/img/Objective.png
category: life
tags:
  - books
  - read
author: myrondza
paginate: true
---

# Optimization Theory

## Root-finding algorithms

In mathematics and computing, a root-finding algorithm is an algorithm for finding zeroes, also called "roots", of continuous functions.

 A zero of a function f, from the real numbers to real numbers or from the complex numbers to the complex numbers, is a number x such that f(x) = 0.

 <img src="https://s3-us-west-2.amazonaws.com/courses-images/wp-content/uploads/sites/3896/2019/04/15194834/Even-Root-Function-Graphic.png" height=200 width=400>

 As, generally, the zeroes of a function cannot be computed exactly nor expressed in closed form, root-finding algorithms provide approximations to zeroes, expressed either as floating point numbers or as small isolating intervals, or disks for complex roots.

 Solving an equation f(x) = g(x) is the same as finding the roots of the function h(x) = f(x) – g(x). Thus root-finding algorithms allow solving any equation defined by continuous functions. However, most root-finding algorithms do not guarantee that they will find all the roots; in particular, if such an algorithm does not find any root, that does not mean that no root exists.



## --- Unconstrained Nonlinear

### 1) Function 
<br>

### a) Golden-section search

Clearly, brute force is not the best way to find the minimum of a function on an interval. A better way would be to divide the given
interval into smaller intervals, then test those to see where the minimum occurs.

We need three points to verify that a minimum lies within an interval. If you just take the midpoint of the interval. Then you still don’t know if the actual minimum lies left or right of the endpoint.

Instead, we divide the interval into three sections instead of two by choosing two interior points instead of one.


The Golden Ratio, symbolized by φ (the Greek letter phi) is a famous number related to the Fibonacci numbers.
It is irrational and has two possible values: 1.61803 and 0.61803. The non-decimal representation is (–1+√5)/2. 
It has the interesting property that φ2 = 1–φ, among others. 

Dividing a segment with these proportions is known as creating a Golden Section.

After dividing the segment, there are two testable intervals, left and right. Whichever one has the middle point lower than the two endpoints, becomes our new interval for the minimum.

Then we will repeat the procedure again.

The cool property of the Golden Ratio is that if we use the exact value of φ, one of the two interior points can be used again – it’s already there. 

<img src="https://upload.wikimedia.org/wikipedia/commons/8/8a/Golden_Section_Search_finding_minimum_value.gif">

<br>
<br>

### b) Interpolation methods (Powell's method)

Powell's conjugate direction method is an algorithm proposed by Michael J. D. Powell for finding a local minimum of a function. The function need not be differentiable, and no derivatives are taken.

The caller passes in the initial point. The caller also passes in a set of initial search vectors. Typically N search vectors are passed in which are simply the normals aligned to each axis.

This method minimises the function by a bi-directional search along each search vector, in turn. The bi-directional line search along each search vector can be done by Golden-section search or Brent's method.



<img src="https://www.researchgate.net/profile/Ting-Yang/publication/307891614/figure/fig8/AS:669690468782094@1536678058822/a-Sequence-of-accepted-points-generated-by-Powells-method-for-a-2D-optimization.png">



### c) Line search

An algorithm is a line search method if it seeks the minimum of a defined nonlinear function by selecting a reasonable direction vector that, when computed iteratively with a reasonable step size, will provide a function value closer to the absolute minimum of the function. Varying these will change the "tightness" of the optimization. 


<img src="https://i.stack.imgur.com/5oxQI.png">
<img src="https://qphs.fs.quoracdn.net/main-qimg-5fbfc1b817c6b57e6c2ee026a1b17e83">

<br>
<br>

### d) Nelder–Mead method

Nelder-Mead is an optimization algorithm named after the developers of the technique, John Nelder and Roger Mead.
Nelder-Mead is a pattern search optimization algorithm, which means it does not require or use function gradient information and is appropriate for optimization problems where the gradient of the function is unknown or cannot be reasonably computed.

A starting point must be provided to the algorithm, which may be the endpoint of another global optimization algorithm or a random point drawn from the domain.
The algorithm works by using a shape structure (called a simplex) composed of n + 1 points (vertices), where n is the number of input dimensions to the function.


The points of the shape structure are evaluated and simple rules are used to decide how to move the points of the shape based on their relative evaluation. This includes operations such as “reflection,” “expansion,” “contraction,” and “shrinkage” of the simplex shape on the surface of the objective function.

In a single iteration of the Nelder–Mead algorithm, we seek to remove the vertex with the worst function value and replace it with another point with a better value. The new point is obtained by reflecting, expanding, or contracting the simplex along the line joining the worst vertex with the centroid of the remaining vertices. If we cannot find a better point in this manner, we retain only the vertex with the best function value, and we shrink the simplex by moving all other vertices toward this value.

<img src="https://codesachin.files.wordpress.com/2016/01/one-minimum.png?w=504&h=378">

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e4/Nelder-Mead_Rosenbrock.gif/290px-Nelder-Mead_Rosenbrock.gif">

<img src="https://machinelearningmastery.com/wp-content/uploads/2020/09/3D-Surface-Plot-of-the-Ackley-Multimodal-Function.png" width=480 height=400>

1. Reflection

This is the first type of transformation that is tried out. You compute the ‘reflected’ point as:

x_r = c + \alpha (c - x_h) 

\alpha is called the reflection parameter, and is usually equal to 1. x_r is essentially a point on the line joining c and x_h, but located away from x_h. This is done in an attempt to move the simplex in a direction thats away from the sub-optimal region around x_h. For a 2-D problem, heres what reflection looks like:


<img src="https://codesachin.files.wordpress.com/2016/01/neldermead_1.jpg">

2. Expansion

If our luck is great and the reflected point x_r happens to be better than the current best (f(x_r) > f(x_l)), we try to explore the possibility further. In other words, we move a little bit more in the direction of x_r from c, in the hope of finding an even better solution. The expanded point is defined as:

x_e = c + \gamma (x_r - c) 

\gamma is called the expansion parameter, and its value in most implementations is 2. Heres what 2-D Expansion looks like:
This is called ‘greedy optimization‘ – we have replaced the worst point with the better of the two options we had.

<img src="https://codesachin.files.wordpress.com/2016/01/neldermead_2.jpg">


3. Contraction

Suppose our reflection point was worst than x_s (i.e. the second worst point). In that case, we need to realise that the direction defined by x_r may not be the ideal one for moving. Therefore, we end up contracting our simplex.

The contraction point x_c is defined as:

x_c = c + \beta (x_h - c) 

\beta is called the contraction parameter, and is usually equal to 0.5. 


<img src="https://codesachin.files.wordpress.com/2016/01/neldermead_3.jpg">

4. Shrink contraction

In this case, we redefine the entire simplex. We only keep the best point (x_l), and define all others with respect to it and the previous points. The jth new point, will now be defined as:

x_j = x_l + \delta (x_j - x_l) 

\delta is called the shrinkage parameter, and is equal to 0.5 in most implementations. What we are essentially doing with the above definition, is moving each point in the simplex towards the current best point, in the hope of converging onto the best neighbourhood. A 2-D Shrinking transformation looks like:


<img src="https://codesachin.files.wordpress.com/2016/01/neldermead_5.jpg">

<br>
<br>

### e) Successive parabolic interpolation

Successive parabolic interpolation is a single variable unbounded optimization method that can also be used as a line search in multivariable problems. The method fits a quadratic function to three points of the function f(x) that you are trying to optimize. Using the quadratic fit it then takes a guess of the optimum of f(x) with the optimum of the fitted quadratic. 

This is repeated, replacing the oldest guess of the optimum with the new guess until converged. This method is typically faster than a golden section search but it may not find an optimum. It can find either a minimum or a maximum without modifying the method.

<img src= "https://www.researchgate.net/profile/Francois-Xavier-Standaert/publication/300641707/figure/fig3/AS:353249472335874@1461232645214/Successive-parabolic-interpolations.png">

<br>
<br>


1. Trust region: minimize a q(δ) only for δ sufficiently small, i.e. in a
“trust region.” For example, a common choice is a spherical trust region
kδk2 < rk
for some radius r
k
, in which case there is a nice result: strong
duality holds, and we can optimize a convex dual problem.1
If the resulting
step is not “acceptable” (see below), we can change the trust-region radius
and try again.
2. Line search: We can minimize f(x
k + αδk
) over α ∈ R, i.e. along the
direction of the Newton step δ
k
. Usually minimizing this exactly is more
trouble than it is worth just to take a single optimization step, so it is
common to do an inexact line search: try different α until the result is
“acceptable” (see below).
3. Backtracking: Instead of exact line search, we try f(x
k + αδk
) for α =
1, τ, τ 2
, τ 3
, . . . where 0 < τ < 1 is some parameter (e.g. τ = 0.5), until the
result is “acceptable” (see below).


### 2) Hessian (Newton's Method)	

Duality plays a very fundamental role in designing second-order methods for convex optimization. Newton’s
method is a second-order method in the simplest setting where we consider unconstrained smooth convex
optimization (same as the setting for gradient descent). 

The idea is to start with an initial guess which is reasonably close to the true root, then to approximate the function by its tangent line using calculus, and finally to compute the x-intercept of this tangent line by elementary algebra. This x-intercept will typically be a better approximation to the original function's root than the first guess, and the method can be iterated.

In gradient descent, the update in the kth iteration, x ˆ (k) moved in the direction of the negative
gradient of the previous iteration

In contrast, in Newton’s method we move in the direction of negative Hessian
inverse of the gradient.

This is called the pure Newton’s method, since there’s no notion of a step size involved. As is evident from
the update, Newton’s method involves solving linear systems in the Hessian.

Say our current location in parameter space is the vector 𝑥0. We can approximate 𝑓 in the vicinity of 𝑥0 using the second order Taylor series expansion:

<img src="https://latex.codecogs.com/png.latex?%5Cbg_white%20f%28x%29%20%5Capprox%20f_T%28x%29%20%3D%20f%28x_0%29%20&plus;%20%28x-x_0%29%5ET%20%5Cnabla%20f%28x_0%29%20&plus;%20%5Cfrac%7B1%7D%7B2%7D%28x-x_0%29%5ET%20H%28x_0%29%20%28x-x_0%29">

This is a quadratic function whose value at 𝑥0, as well as its first and second partial derivatives, match those of 𝑓. ∇𝑓(𝑥0) is the gradient of 𝑓 evaluated at 𝑥0. This is a vector containing the partial derivatives of 𝑓, and is analogous to the derivative for functions of single variables. Similarly, 𝐻(𝑥0) is the Hessian of 𝑓 evaluated at 𝑥0. It's a matrix containing second partial derivatives of 𝑓, and is analogous to the second derivative for functions of single variables.


Minimizing the local approximation

Given the local approximation 𝑓𝑇 at the current point 𝑥0, we want to find a new point 𝑥 that minimizes 𝑓𝑇. This can be done in closed form by taking the gradient of 𝑓𝑇 with respect to 𝑥, setting it to zero, then solving for 𝑥.

The gradient of 𝑓𝑇 can be found by differentiating the expression above (keeping in mind that ∇𝑓(𝑥0) is just a fixed vector and 𝐻(𝑥0) is just a fixed matrix):

<img src="https://latex.codecogs.com/png.latex?%5Cbg_white%20%5Cnabla%20f_T%28x%29%20%3D%20%5Cnabla%20f%28x_0%29%20&plus;%20H%28x_0%29%20%28x%20-%20x_0%29">

Setting it to zero, we have:

<img src="https://latex.codecogs.com/png.latex?%5Cbg_white%20H%28x_0%29%20%28x%20-%20x_0%29%20%3D%20-%5Cnabla%20f%28x_0%29">

We need to isolate 𝑥, so multiply both sides by the inverse of the Hessian, then move 𝑥0 to the righthand side:

<img src="https://latex.codecogs.com/png.latex?%5Cbg_white%20x%20%3D%20x_0%20-%20%5CBig%28%20H%28x_0%29%20%5CBig%29%5E%7B-1%7D%20%5Cnabla%20f%28x_0%29">

<br>
<br>

<img src="https://tutorial.math.lamar.edu/classes/calci/NewtonsMethod_Files/image001.png">

1. Select starting point x0, and convergence parameter εg.
2. Compute g(xk) ≡ ∇f(xk). If kg(xk)k ≤ εg then stop. Otherwise, continue.
3. Compute H(xk) ≡ ∇2
f(xk) and the search direction, pk = −H−1
gk.
4. Perform line search to find step length αk in the direction of pk (start with αk = 1).
5. Update the current point, xk+1 = xk + αkpk and return to step 2.


<img src="https://qphs.fs.quoracdn.net/main-qimg-e908f9721cc82415fa7e70c763351f3a" height=400 width=450>


### 3) Gradient (Quasi–Newton's Method)	

The problem with Newton steps is that the exact Hessian is hard to come by when n is large. Even with adjoint methods, evaluating H exactly typically costs at least n times the cost of evaluating f once (it correspond to taking the gradient n times: one more gradient for each component of ∇f). When n is really large, just storing the H matrix (nˆ2 numbers) might be impractical.

Instead, “quasi” Newton methods (also called “variable-metric” methods) apply the same Newton steps above but use an approximate Hessian Hk, often a low-rank approximation (which can be stored and applied efficiently). In fact, since what is needed for the Newton step is (Hk)−1, usually one stores a lowrank approximate inverse Hessian. To obtain this, we want to iteratively construct our approximate Hk+1 (or (Hk+1)−1) given only the gradient (firstderivative) of f.


<img src="https://upload.wikimedia.org/wikipedia/commons/a/ad/Sekantenverfahren_Ani2.gif" height=400 width=450>
<br>

### a) Berndt–Hall–Hall–Hausman

The Berndt–Hall–Hall–Hausman (BHHH) algorithm is a numerical optimization algorithm similar to the Newton–Raphson algorithm, but it replaces the observed negative Hessian matrix with the outer product of the gradient. This approximation is based on the information matrix equality and therefore only valid while maximizing a likelihood function.

If a nonlinear model is fitted to the data one often needs to estimate coefficients through optimization. A number of optimisation algorithms have the following general structure. Suppose that the function to be optimized is Q(β). Then the algorithms are iterative, defining a sequence of approximations, βk given by

<img src="https://latex.codecogs.com/png.latex?%5Cbg_white%20%5Cbeta_%7Bk&plus;1%7D%20%3D%20%5Cbeta_%7Bk%7D%20-%20%5Clambda_%7Bk%7DA_%7Bk%7D%20%5Cfrac%7B%5Cpartial%20Q%7D%7B%5Cpartial%20B%7D%20%28%5Cbeta_%7Bk%7D%20%29">

where βk is the parameter estimate at step k, and lambda k is a parameter (called step size) which partly determines the particular algorithm. For the BHHH algorithm λk is determined by calculations within a given iterative step, involving a line-search until a point βk+1 is found satisfying certain criteria.


<img src="https://latex.codecogs.com/png.latex?%5Cbg_white%20A_%7Bk%7D%20%3D%20%5Cleft%20%5B%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20%5Cfrac%7B%5Cpartial%20%5Cln%20Q_%7Bi%7D%7D%7B%5Cpartial%20%5Cbeta%20%7D%20%28%5Cbeta_%7Bk%7D%20%29%20%5Cfrac%7B%5Cpartial%20%5Cln%20Q_%7Bi%7D%7D%7B%5Cpartial%20%5Cbeta%20%7D%20%28%7B%5Cbeta_%7Bk%7D%20%7D%29%27%20%5Cright%20%5D%5E%7B-1%20%7D">

### b) Broyden–Fletcher–Goldfarb–Shanno and L-BFGS

It is a type of second-order optimization algorithm, meaning that it makes use of the second-order derivative of an objective function and belongs to a class of algorithms referred to as Quasi-Newton methods that approximate the second derivative (called the Hessian) for optimization problems where the second derivative cannot be calculated.

The BFGS algorithm uses a line search in the chosen direction to determine how far to move in that direction.

Limited Memory BFGS (or L-BFGS) is an extension to the BFGS algorithm that addresses the cost of having a large number of parameters. It does this by not requiring that the entire approximation of the inverse matrix be stored, by assuming a simplification of the inverse Hessian in the previous iteration of the algorithm (used in the approximation).

It does so by gradually improving an approximation to the Hessian matrix of the loss function, obtained only from gradient evaluations (or approximate gradient evaluations) via a generalized secant method.

The BFGS Hessian approximation can either be based on the full history of gradients, in which case it is referred to as BFGS, or it can be based only on the most recent m gradients, in which case it is known as limited memory BFGS, abbreviated as L-BFGS. The advantage of L-BFGS is that is requires only retaining the most recent m gradients, where m is usually around 5 to 20, which is a much smaller storage requirement than n*(n+1)/2 elements required to store the full (triangle) of a Hessian estimate, as is required with BFGS, where n is the problem dimension.


<img src="https://ars.els-cdn.com/content/image/1-s2.0-S0097849314000119-gr1.jpg">

<img src="https://i.stack.imgur.com/t39X3.png" width=370 height=300>


### c) Davidon–Fletcher–Powell

One of the first quasi-Newton methods was devised by Davidon (1959) and modified by Fletcher
and Powell (1963).
Suppose we model the objective function as a quadratic at the current iterate xk:

Instead of computing Bk “from scratch” at every iteration, a quasi-Newton method updates it
in a way that accounts for the curvature measured during the most recent step. We want to
build the quadratic model,


<img src="https://www.mathworks.com/matlabcentral/mlc-downloads/downloads/submissions/23543/versions/1/screenshot.jpg">

1. Select starting point x0, and convergence parameter εg. Set k = 0 and V0 = I.
2. Compute g(xk) ≡ ∇f(xk). If kg(xk)k ≤ εg then stop. Otherwise, continue.
3. Compute the search direction, pk = −Vkgk.
4. Perform line search to find step length αk in the direction of pk (start with αk = 1).
5. Update the current point, xk+1 = xk + αkpk, set sk = αkpk, and compute the change in
the gradient, yk = gk+1 − gk.
6. Update Vk+1 by computing
Ak =
Vkyky
T
k Vk
y
T
k Vkyk
Bk =
sks
T
k
s
T
k
yk
Vk+1 = Vk − Ak + Bk
7. Set k = k + 1 and return to step 2.

### d) Symmetric rank-one (SR1)

If we drop the requirement that the approximate Hessian (or its inverse) be positive definite, we
can derive a simple rank-1 update formula for Bk that maintains the symmetry of the matrix
and satisfies the secant equation. Such a formula is given by the symmetric rank-1 update (SR1)
method (we use the Hessian update here, and not the inverse Vk)

Why would we be interested in a Hessian approximation that is potentially indefinite? In practice,
the matrices produced by SR1 have been found to approximation the true Hessian matrix very
well (often better than BFGS). This may be useful in trust-region methods (see next section)
or constrained optimization problems; in the latter case the Hessian of the Lagrangian is often
indefinte, even at the minimizer.

To use the SR1 method in practice, it may be necessary to add a diagonal matrix γI to Bk
when calulating the serach direction, as was done in modified Newton’s method. In addition, a
simple back-tracking line search can be used, since the Wolfe conditions are not required as part
of the update (unlike BFGS)
<br>
<br>

### 4) Other Methods
<br>

### a) Conjugate gradient

In mathematics, the conjugate gradient method is an algorithm for the numerical solution of particular systems of linear equations, namely those whose matrix is positive-definite. The conjugate gradient method is often implemented as an iterative algorithm, applicable to sparse systems that are too large to be handled by a direct implementation or other direct methods such as the Cholesky decomposition.


• Dense direct(factor-solve methods)
Runtime depends only on size; independent of data, structure, or sparsity
Work well fornup to a few thousand

• Sparse direct(factor-solve methods)
Runtime depends on size, sparsity pattern; (almost) independent of data
Can work well fornup to 10ˆ4 or 10ˆ5 (or more)
Requires good heuristic for ordering

• Indirect(iterative methods)
runtime depends on data, size, sparsity, required accuracy
requires tuning, preconditioning,
good choice in many cases; only choice forn= 10ˆ6 or large


<img src="https://fmin.xyz/docs/methods/adaptive_metrics/steepest.png" height=400 width=450>

<img src="https://www.researchgate.net/profile/Tapani-Raiko/publication/221533635/figure/fig1/AS:669971994656777@1536745179310/Gradient-and-conjugate-gradient-updates-are-applied-to-finding-the-maximum-of-the.png" height=400 width=450>

If we move in a direction until the directional derivative in that direction is zero (equivalently, the gradient is orthogonal to the direction we are traveling) then the minimum falls somewhere on the plane orthogonal to our direction! In other words, we are done with traveling in that direction.

Conjugate gradient descent is a method where directions are chosen in a way that makes it less likely that you have to walk in the same direction at a later iteration thus making sure you can reach the bottom in fewer slope measurements.

### b) Gauss–Newton

The Gauss-Newton method is an iterative algorithm to solve nonlinear least squares problems. “Iterative” means it uses a series of calculations (based on guesses for x-values) to find the solution. It is a modification of Newton’s method, which finds x-intercepts (minimums) in calculus. The Gauss-Newton is usually used to find the best fit theoretical model although it could also be used to locate a single point.

This algorithm is probably the most popular method for non-linear least squares. It does however, have a few pitfalls:

If you don’t make a good initial guess, it will be very slow to find a solution and may not find one at all.
The procedure is not-suited for design matrices that are ill-conditioned or deficient in rank.
If relative residuals are very big, the procedure will lose a large amount of information.

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a8/Regression_pic_assymetrique.gif/600px-Regression_pic_assymetrique.gif" height=400 width=450>


### c) Gradient Descent

Gradient descent is an optimization algorithm that's used when training a machine learning model. It's based on a convex function and tweaks its parameters iteratively to minimize a given function to its local minimum.

A gradient simply measures the change in all weights with regard to the change in error. You can also think of a gradient as the slope of a function. The higher the gradient, the steeper the slope and the faster a model can learn. But if the slope is zero, the model stops learning. In mathematical terms, a gradient is a partial derivative with respect to its inputs.

Instead of climbing up a hill, think of gradient descent as hiking down to the bottom of a valley. This is a better analogy because it is a minimization algorithm that minimizes a given function.

The equation below describes what gradient descent does: b is the next position of our climber, while a represents his current position. The minus sign refers to the minimization part of gradient descent. The gamma in the middle is a waiting factor and the gradient term ( Δf(a) ) is simply the direction of the steepest descent.

So this formula basically tells us the next position we need to go, which is the direction of the steepest descent. Let's look at another example to really drive the concept home. 

Imagine you have a machine learning problem and want to train your algorithm with gradient descent to minimize your cost-function J(w, b) and reach its local minimum by tweaking its parameters (w and b). 

We know we want to find the values of w and b that correspond to the minimum of the cost function (marked with the red arrow). To start finding the right values we initialize w and b with some random numbers. Gradient descent then starts at that point (somewhere around the top of our illustration), and it takes one step after another in the steepest downside direction (i.e., from the top to the bottom of the illustration) until it reaches the point where the cost function is as small as possible.

<img src="https://thumbs.gfycat.com/AngryInconsequentialDiplodocus-size_restricted.gif" height=400 width=450>

### d) Levenberg–Marquardt

In mathematics and computing, the Levenberg–Marquardt algorithm (LMA or just LM), also known as the damped least-squares (DLS) method, is used to solve non-linear least squares problems. These minimization problems arise especially in least squares curve fitting.

The LMA is used in many software applications for solving generic curve-fitting problems. However, as with many fitting algorithms, the LMA finds only a local minimum, which is not necessarily the global minimum. The LMA interpolates between the Gauss–Newton algorithm (GNA) and the method of gradient descent. The LMA is more robust than the GNA, which means that in many cases it finds a solution even if it starts very far off the final minimum. For well-behaved functions and reasonable starting parameters, the LMA tends to be slower than the GNA. LMA can also be viewed as Gauss–Newton using a trust region approach. 

<img src="https://i.stack.imgur.com/eMUwY.gif" height=400 width=450>

### e) Powell's dog leg method

Powell's dog leg method is an iterative optimisation algorithm for the solution of non-linear least squares problems

Similarly to the Levenberg–Marquardt algorithm, it combines the Gauss–Newton algorithm with gradient descent, but it uses an explicit trust region. At each iteration, if the step from the Gauss–Newton algorithm is within the trust region, it is used to update the current solution. If not, the algorithm searches for the minimum of the objective function along the steepest descent direction, known as Cauchy point. If the Cauchy point is outside of the trust region, it is truncated to the boundary of the latter and it is taken as the new solution. If the Cauchy point is inside the trust region, the new solution is taken at the intersection between the trust region boundary and the line joining the Cauchy point and the Gauss-Newton step (dog leg step).

<img src="https://d3i71xaburhd42.cloudfront.net/346761f6189f7dd8db2d32b0c14065c3bc01a65d/3-Figure1-1.png" height=200 width=350>

### f) Truncated Newton

Truncated Newton methods, also known as Hessian-free optimization,[1] are a family of optimization algorithms designed for optimizing non-linear functions with large numbers of independent variables. A truncated Newton method consists of repeated application of an iterative optimization algorithm to approximately solve Newton's equations, to determine an update to the function's parameters. The inner solver is truncated, i.e., run for only a limited number of iterations.

<br>
<br>
## --- Constrained Nonlinear

### a) Barrier methods
### b) Penalty methods

(Differentiable)	
### c) Augmented Lagrangian methods
### d) Sequential quadratic programming
### e) Successive linear programming


## --- Convex optimization

<br>
1) Convex minimization	
<br>

### a) Cutting-plane method
### b) Reduced gradient (Frank–Wolfe)
### c) Subgradient method


<br>
2) Interior point	
<br>

### a) Affine scaling
### b) Ellipsoid algorithm of Khachiyan
### c) Projective algorithm of Karmarkar

<br>
<br>

## --- Combinatorial

### a) Approximation algorithm
### b) Dynamic programming
### c) Greedy algorithm
### d) Integer programming (Branch and bound/cut)


<br>
<br>

*** Minimum spanning tree	

### a) Borůvka
### b) Prim
### c) Kruskal


<br>
<br>

*** Shortest path	

### a) Bellman–Ford SPFA
### b) Dijkstra
### c) Floyd–Warshall

<br>
<br>

## --- Metaheuristics

### a) Evolutionary algorithm
### b) Hill climbing
### c) Local search
### d) Simulated annealing
### e) Tabu search

<br>
<br>

## Code
Example Code

```js
// Example can be run directly in R 


// Example can be run directly in Python


```







