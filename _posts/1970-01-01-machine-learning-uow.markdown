---
layout: post
title:  "Machine Learning - University of Washington"
date:   2015-05-21 23:28:00
categories: public
---

<https://class.coursera.org/machlearning-001>

* Machine learning algorithms are combination of different components. Just learn the components!

* Every machine learning algorithm has three components:
** Representation
** Evaluation
** Optimization : depends on evaluation and representation

# Representation examples

decision trees
: just trees of decisions

set of rules / logic programs
: like decision trees but not nested. chain mechanism
 
instances
: remember the cases you saw. when a new case comes out, find the closest case you've seen. like a doctor's diagnosis.

graphical models
: Bayes/Markov nets. Probability. 

Neural networks
: you know it

Support vector machines
: TBD 

Model ensembles
: combining representations

# Evaluation measure examples

Accuracy
: how much of my guess was right
: how much percentage of labels of mine as spam and not spam were right?
 
Precision and recall
: to find out false positives and false negatives.
: precision : how much percentage of the mails I labelled as spam were spams out of real spams?
: recall: how much percentage of the mails I labelled as spam were spam out of all emails? 

Squared error
: sum of all errors

Likelihood
: how likely is what you see according to your model

Posterior probability
: combination of likelihood and priori 

Cost / Utility
: false positives are often costly than false negatives. that means, accuracy is not everything.
: marking a non-spam mail as spam is worse than not marking a spam as spam 

Margin
: when you make boundary, how close you're to the real line

Entropy
: information content as a variable

K-L divergence
: TBD


# Optimization examples

combinatorial optimization
: e.g. greedy search. Used on discrete model.

convex optimization
: e.g. gradient descent. Used on continuous model.

constrained optimization
: e.g. linear programming. combination of combinatorial and convex optimization.


# Types of learning

supervised (inductive)
: largest, most mature type of ML. training data includes desired outputs.

unsupervised learning
: training data does not include desired outputs. example: clustering customers like teenagers X middle age people

semi-supervised learning
: training data includes a few desired outputs. you cannot afford label all data; just some of them. then label existing data.

reinforcement learning
: rewards from sequence of actions. hardest one. no point-by-point decisions. sequence of decisions.
 

# ML in practice

* Understanding domain, prior knowledge and goals: learn the problem, learn the goal
* Data integration, selection, cleaning, pre-processing 
* Learning models: come up with a model from data/domain.
* Interpreting results: are you satisfied with the result?                              
* Consolidating and deploying discovered knowledge: Use the model in reality.  
* Go step #0


# Supervised learning = Inductive learning
 
* Given examples of a function (X, F(X)) : X-> input, F(x)-> output
* Predict function F(X) for new examples X
** Discrete F(X): Classification
** Continuous F(X): Regression
** If F(X) is probability(X) : Probability estimation. Regression with outcomes that add up to 1

















