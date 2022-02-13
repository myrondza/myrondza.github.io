---
date: 2018-10-09 12:26:40
layout: post
title: Causal Inference
subtitle: Causal Inference
description: Here we understand the fundamental concepts of Causal Inference. As well as we look at the newly emerged Causal Inference framework libraries - DoWhy (Assumptions) & EconML (Estimations).
image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRf-UbkdSVY-IwrVKmEgI4j7VDxfiJiQMdm2Q&usqp=CAU
optimized_image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRf-UbkdSVY-IwrVKmEgI4j7VDxfiJiQMdm2Q&usqp=CAU
category: css
tags:
  - css
  - tips
author: myrondza
---
# Causal Inference

<p>
<img src="https://dnarobotics.files.wordpress.com/2017/11/ms_logo_cam.gif" height=70>
<img src = "https://econml.azurewebsites.net/_static/econml-logo-inverse.png" height=70>
  
  What is a Causal Relationship?

A causal relationship describes a relationship between two variables such that one has caused another to occur. It is a much stronger relationship than correlation, which is just describing the co-movement patterns between two variables. 

Confounding Variable : A confounding variable (confounder) is a factor other than the one being studied that is associated both with the outcome (dependent variable) and with the factor being studied (independent variable). 

Instrument Variable : An instrument variable is the variable that is highly correlated with the independent variable X but is not directly correlated with the dependent variable Y. 


<img src ="https://miro.medium.com/max/700/1*Pj34vjHFrO0fIBh8G56U5g.png" height= 200>

For causality, However, it is a much more complicated relationship to capture. To know whether variable A has caused variable B to occur, i.e., whether treatment A has caused outcome B, we need to hold all other variables constant to isolate and quantify the effect of the treatment. The other variables that we need to control are called confounding variables, which are the variables that are correlated with both the treatment and the outcome.

<img src="https://ars.els-cdn.com/content/image/1-s2.0-S2095809919305235-ga1.jpg">

  
Potential Outcomes
• Each unit (individual) has two potential outcomes:
– Y0 is the potential outcome had the unit not been treated:
“control outcome”
– Y1 is the potential outcome had the unit been treated:
“treated outcome”        
 
 
 
Typical assumption 
Y0 Y1: potential outcomes for control and treated
X: unit covariates (features)
T: treatment assignment

Potential outcomes framework
– Average treatment effect (ATE)

On average, what is the difference in the outcome variable between the treatment group and the control group?

• Assuming ignorability, we will derive the
adjustment formula (Hernán & Robins 2010,
Pearl 2009)
• The adjustment formula is extremely useful in
causal inference
• Also called G-formula
   
           
Average Treatment Effect
The expected causal effect of T on Y: 
ATE := E [Y1 - Y0]

– Conditional average treatment effect (CATE)

The conditional average treatment effect is estimating ATE applying some condition x. In some cases, the treatment will generate different effects on different subgroups, and ATE can be zero because the effects are canceled out. CATE can be useful for estimating heterogeneous effects among subgroups
  
  

<img src="https://www.sciencenewsforstudents.org/wp-content/uploads/2021/03/1030_SS_neuron_feat.jpg" height=300 width=500>

A decision requires making a “causal inference,” that is, an inference as to whether two sensory signals derive from a common source or separate sources.
  
<img src="https://dnarobotics.files.wordpress.com/2017/11/ms_logo_cam.gif">
  
## DoWhy (Assumptions)
 It is designed to highlight the critical but often neglected assumptions underlying causal inference analyses. DoWhy does this by first making the underlying assumptions explicit, for example, by explicitly representing identified estimands. And secondly by making sensitivity analysis and other robustness checks a first-class element of the causal inference process.

Goal : Identifying assumptions for causal inference
  
  
## Econ ML (Estimation)
It applies the power of machine learning techniques to estimate individualized causal responses from observational or experimental data.
By reducing the need for expert judgment, these innovations improve the reliability of what-if predictions and empower data scientists without extensive economic training to conduct causal analysis using existing data.
  
  
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ2np2Ab3Fds1ncko1zshDsiOMPu9Y7m-iiPA&usqp=CAU">
  
  
 ## Estimation Methods under Unconfoundedness
Methods for estimating (heterogeneous) treatment effects, whose theoretical guarantees are valid only when all potential confounders/controls (factors that simultaneously had a direct effect on the treatment decision in the collected data and the observed outcome) are observed.

### Orthogonal/Double Machine Learning

Double Machine Learning is a method for estimating (heterogeneous) treatment effects when all potential confounders/controls (factors that simultaneously had a direct effect on the treatment decision in the collected data and the observed outcome) are observed, but are either too many (high-dimensional) for classical statistical approaches to be applicable or their effect on the treatment and outcome cannot be satisfactorily modeled by parametric functions (non-parametric).

The method reduces the problem to first estimating two predictive tasks:

Predicting the outcome from the controls,

Predicting the treatment from the controls

### Doubly Robust Learning

Thus unlike Double Machine Learning the first model predicts the outcome from both the treatment and the controls as opposed to just the controls. Then the method combines these two predictive models in a final stage estimation so as to create a model of the heterogeneous treatment efffect.

It reduces the problem to first estimating two predictive tasks:

Predicting the outcome from the treatment and controls,

Predicting the treatment from the controls

### Forest Based Estimators

Different estimation methods provided in the package that use a forest based methodology to model the treatment effect heterogeneity.

These estimators, similar to the DML and DR sections require the unconfoundedness assumption, i.e. that all potential variables that could simultaneously have affected the treatment and the outcome to be observed.

### Metalearners 

Meta-learner they simply combine ML methods in a black box manner so as to get a final stage estimate and do not introduce new estimation components.

Metalearners are discrete treatment CATE estimators that model either two response surfaces, 𝑌(0) and 𝑌(1), or multiple response surfaces, 𝑌(0) to 𝑌(𝐾) separately.

The T-Learner models 𝑌(0), 𝑌(1) separately.The outcome models for the control and treatment group, respectively. Here, 𝑀0, 𝑀1 can be any suitable machine learning algorithms that can learn the relationship between features and outcome.

<img src= "https://matheusfacure.github.io/python-causality-handbook/_images/t-learner.png">

The S-Learner models 𝑌(0) and 𝑌(1) through one model that receives the treatment assignment 𝑇 as an input feature (along with the features 𝑋).

<img src ="https://matheusfacure.github.io/python-causality-handbook/_images/s-learner.png">

The X-Learner models 𝑌(1) and 𝑌(0) separately in order to estimate the CATT (Conditional Average Treatment Effect on the Treated) and CATC (Conditional Average Treatment Effect on the Controls). The CATE estimate for a new point 𝑥 is given by the propensity-weighted average of CATT and CATC.

<img src="https://matheusfacure.github.io/python-causality-handbook/_images/x-learner.png">

## Estimation Methods with Instruments

Methods for estimating (heterogeneous) treatment effects, even when there are unobserved confounders (factors that simultaneously had a direct effect on the treatment decision in the collected data and the observed outcome). However, the methods assumes that we have access to an instrumental variable: a random variable that had an effect on the treatment, but did not have any direct effect on the outcome, other than through the treatment.
 
<img src ="https://www.microsoft.com/en-us/research/uploads/prod/2018/08/Figure1_DoWhy.-Separating-indentification-and-estimation-of-casual-effect-1024x417.png" height="200">
  
# A/B Testing
  
A/B testing is the act of running a simultaneous experiment between two or more variants of a page to see which one performs the best.

By sending half your traffic to one version of the page and half to another, you can first gather evidence about which one works best before you commit to the change.

Ideally, the business would run A/B tests between the old and new versions of the website. However, a direct A/B test might not work because the business cannot force the customers to take the new offering. Measuring the effect in this way will be misleading since not every customer exposed to the new offering will take it.

 On one hand, the DoWhy library can help build a causal model, identify the causal effect and test causal assumptions. On the other hand, EconML's  Estimator can estimate heterogeneous treatment effects by taking advantage of the fact that not every customer who was offered the new features was more likely to convert. Furthermore, EconML provides users tools to understand causal effects and make causal policy decisions.
  
<img src= "https://static.wingify.com/gcp/uploads/2021/05/1.png">
  

  
