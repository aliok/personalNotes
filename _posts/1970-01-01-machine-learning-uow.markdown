---
layout: post
title:  "Machine Learning - University of Washington"
date:   2015-05-21 23:28:00
categories: public
---

<https://class.coursera.org/machlearning-001>

Terminology:
===============================================================================================
training example
: An input-output pair `<x, f(x)>`

Target function / target concept
: true function we want to learn `f`. this is not accessible.

Hypothesis
: Proposed function `h` believed to be similar to `f`. Candidate function

Concept
: A boolean function. If hypothesis is boolean.
 
Positive example / positive instance
: Examples for which `f(x)=1` are called

Classifier
: Discrete-valued function. Like a spam filter that says "this is spam" and "this is not spam".

Class / class label / label
: Possible values `f(x)` in `{1,....,K}`

Hypothesis space
: Spaces of all hypotheses that can be output by a learning algorithm.
 
Version space
: Space of all hypotheses that have not yet been ruled out by a training example. Subset of the hypothesis space. Shrinks when finding new examples.
 
Overfitting
: My current model/algorithm is matching perfectly. But, what can I do to optimize accuracy on future data points?
: Accuracy I want is not on training data, but on test data. 


 
Introduction
===============================================================================================

* Machine learning algorithms are combination of different components. Just learn the components!

* Every machine learning algorithm has three components:
  * Representation
  * Evaluation
  * Optimization : depends on evaluation and representation

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


Supervised learning = Inductive learning
===============================================================================================================
 
* Given examples of a function `(x, f(x))` : `x`-> input, `f(x)`-> output
* Predict function `f(x)` for new examples X
  * Discrete `f(x)`: Classification
  * Continuous `f(x)`: Regression
  * If `f(x)` is `probability(X)` : Probability estimation. Regression with outcomes that add up to 1

#### Examples:
* Credit risk assessment
  * `x`    : properties of customer and proposed purchase
  * `f(x)` : approve purchase or not

#### Appropriate situations
* No human expert: 
  * predicting binding strength of new molecule to AIDS protease molecule
* Humans can perform the task, but can't describe how
  * hand writing recognition
* Desired function is changing frequently
  * stock predictions
* Each user needs a customized function `f`
  * spam classification, book recommendation
 

#### Hypothesis spaces
* Complete ignorance: We know nothing or very little about the output. 
  * e.g. a boolean function that we only know 2 input-output pairs but there are 4 parameters which means we complete input-output pairs would be 2^4=16
* Simple rules: easy conjunction functions 
* m-of-n rules: if m of n rules are true, then we have our rule.
  * like a medical diagnosis system. one might not have some symptoms.




Decision trees
==========================================================================================
* Hypothesis space:
  * Variable size: Size of the tree grows with the amount of data we have   
  * Deterministic: For each example you're positive or negative
  * Discrete and continuous parameters: Discrete params are choices. Continuous params would be sth like probabilities.
* In X-Y 2 dimensional space: decision trees can't match a line. It outputs small rectangles. Or in 3D, it outputs small cubes.

#### Building a decision tree
* Start with most important feature
* Then you have a left tree and right tree
* Then pick the next most important feature on left tree
* Then pick the next most important feature on right tree
* Recurse ...
* Selecting the most important feature
  * Simplest way to find out is pick the attribute that has lowest error rate when used alone.
  * Another method is picking the one that has best information gain (entropy)

##### Entropy
* Surprise, `S(V=v)` of each value of V defined to be 
    `S(V=v) = -lg P(V=v)` where `P` is a probability distribution. 
* Entropy = average surprise. Measure of uncertainty.
  * A fair coin has higher entropy than a cheating one. You're always surprised when both possibilities are equal.

##### Non-boolean functions
* Construct a multiway split:
    
        ROOT
       / |  \
      A  B  C

* Test for one versus all others:

           ROOT
         /      \
        A       !A
       / \      / \
      B  !B    B   !B

* Group the values into two disjoint subsets:

           ROOT
         /      \
       A or B   C or D
       
       

       
<style>
/** Some special overrides for this page **/
@include media-query($on-laptop) {
    blockquote{
        color: inherit;
        font-style: inherit;
        letter-spacing:inherit;
    }

    dt{
        width: 250px;
    }

    dd{
        margin-left: 270px;
    }
}
</style>