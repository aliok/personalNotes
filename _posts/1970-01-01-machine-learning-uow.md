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

# Search prodecures
* Greedy search
* Round-robin replacement
* Backfitting
* Beam search


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
       
##### Unknown attribute values
Example: you have 2 types of attributes but attr#2 is only available on a small subset. What would you do?

Different options:

1. Assign most common value of attr#2 for missing ones.
2. Assign most common value of attr#2 for missing ones for attr#1 value.
3. Convert method #2 to a probability method. 
       
##### Overfitting
Overfitting happens when the decision tree fits the training data perfectly but on test data it doesn't fit very good. 
That means, I might have a bad answer for future tests.

For example: my friend didn't want to play tennis on a very good weather because of other reasons that are not in my decision tree (e.g. being sick).
Because of that example, I cannot claim that he doesn't want to play tennis on a good day.
Usually very big trees overfits the training data.

Avoiding:

* Split data into training and test data
* Having a small tree: grow full tree then post-prune (budamak). 
  * How to select best tree:
      * Measure performance over training data
      * Measure performance over separate validation data set (separate from test set)
      * Add complexity penalty to performance measure: e.g. increase in size of tree would result in a penalty
  * How to do pruning:
      * Prune the tree based on validation data
      * 2 basic methods: reduced-error pruning and rule post-pruning 

Cross validation: Split data into e.g. 10 subsets. Pick 1 as training and 9 as validation set. Then go to next round (select next set as training).
 This would be a good idea if we have very small data. On big data, there is no need.
 
##### Scaling:
* ID3, CR.5     : random access
* SPRINT, SLIQ  : multiple iterations
* VFTP          : online (data stream) 
       

Rule based learning
===============================================================================================================
Hypothesis space:

* Each rule is a conjunction of tests
* A rule set is disjunction of rules. e.g. all rules are for one class (e.g. 1 if one rule matches, 0 if none matches) 

Rule sets vs decision trees:

* They can be converted to each other. But converting rule sets to decision trees might end up in huge treees because you need to replicate tests.
* It is easier to overfit with rule learning than decision tree learning.  

* Typical search procedure employed is beam search, not plain greedy search.

* Learning rules for multiple classes: Do learning for classes one by one.
    Two possible way to figure out the class of an example:
    * Order rules (decision lists)
    * Weighted vote (e.g., weight = accuracy x coverage)

#### Learning First-Order Rules
Propositional representation: Just booleans
First order logic : Functions, predicates etc. which are like programming

* Can learn set of rules such as:
    * Ancestor(x,y) <-- Parent(x,y)  (base case)
    * Ancestor(x,y) <-- Parent(x,z) and Ancestor (z,y)
        * x is y's ancestor, if there is a z which x is the parent of it and z is
          an ancestor of y
          
* Instead of having rules only for the object, we have rules for the related objects as well

#### FOIL : First-Order Inductive Learner

* Relations etc. --> can be modeled as DB tables
* Rules can be made from relations

#### Induction as Inverted Deduction

* Classical deduction example: Socrates is a man; all men are mortal; thus Socrates is mortal.
* Classical induction example: Socrates is a man; Socrates is mortal; XYZ is a man; XYZ is mortal. Then maybe all men are mortal.
* Deduction vs induction: Go to specific from general vs go to general from specific examples


Instance based learning
==================================================================================================================
* K-nearest neighbor
* Other forms of IBL
* Collaborative filtering

* Instance-based learning
  * Just store all training examples
  * Nearest neighbor: When we have a new instance, scan thru the training examples and find the closest to that one
  * k-nearest neighbor: Find k closest. Each one has a class and they vote (or averaged, or meaned, or weighted-averaged, etc.).
  
* Advantages:
  * Training is very fast
  * Learn complex target functions easily: Once you find neighbors, you implicitly find complex functions 
  * Don't lose information

* Disadvantages:
  * Slow query time. And it goes worse with more data.
  * Lots of storage <-- stores all training examples
  * Easily fooled by irrelevant attributes. But e.g. decision trees find the relevant attributes. 

* Distance measures: How do I define closest? (similarity measure)
  * Numeric features: 
    * Euclidian(straight line distance), Manhattan(sum of the distances), L^n-norm(more advanced version of square root distance)
    * Normalized by: range, std. deviation 
  * Symbolic features (for boolean features):
    * Hamming/overlap: for each feature number of same features
    * Value difference measure(VDM): I have 3 colors RGB. What could possibly make R more similar to G or B? But think about classification. a bit complicated. TBD 
  * In general:
    * Arbitrary, encode knowledge
    
* Voronoi diagram: TBD
* Voronoi cell of x in training set:
  * All points closer to x to any other instance in training set. That means, when we have an instance to test which lies in that cell, class will be that cell's class (x's class).
  * Region of class C: Union of Voronoi cells of instances of class C in training set


* Distance-weighed k-nearest neighbors (k-NN):
  * Closest one has more weight
  * Then, let's use all examples instead of k-closest ones: but it is faster to work on k instances.

* Curse of dimensionality:
  * second biggest problem after overfitting
  * applies everywhere (decision trees, k-NN, etc.)
  * problems:
    * nearest neighbor is easily misled when hi-dim:  
    * easy problems are hard in hi-dim:  
    * low-dim intuitions don't apply in hi-dim: hard to understand in hi-dim
    * e.g. normal distribution:
      * in 1d, most of the mass is around mean
      * in 2d, still some data is around mean
      * but it gets less and less... 
      * hi-dim: most of the mass is far away from the mean.
    * e.g. points on hypergrid: similarity, classes and nearest neighbors become meaningless
      * 1d: equal length lines, 2 nearest neighbors
      * 2d: 2d grid. 4 nearest neighbors
      * Nd: 2*N nearest neighbors.

* Dealing with curse of dimensionality: get rid of some dimensions. called *feature selection* 
  * Filter approach: linear operation that removes features. Very efficient.
    * e.g. by information gain 
  * Wrapper approach: run learner with different combinations of features
    * forward selection
    * backward elimination
    * etc.
    
* Forward selection
  * Start with empty set of features and add useful ones one by one
  * When to stop: all features are in the set or adding a new feature doesn't make the accuracy better
  * More efficient than backward elimination but there are disadvantages as well
* Backward elimination
  * Start with all features and remove useless ones one by one 

* How to decide if a feature is useful or not:
  * how to not remove 100 less useful features when we have 1 very useful feature? 100 of them would make a big difference.
  * *feature weighting* to the rescue!
    * Gradient descent is used for weighting the features. What weights give minimum error? 

* k-NN is said above that it needs all training instances. But that is costly. What to do for reducing computational cost?
  * Efficient retrieval:
    * come up with a good data structure that allows fast retrievel
    * e.g. k-D trees: good with low-dim 
  * Efficient similarity comparison: use cheap approximation to get rid of most of the instances and then do expensive measures on remainder
  * Form prototypes: Come up with prototypes for instances that cover them. Do not deal with details.
  * Edited k-NN: get rid of instances that do not change frontier (e.g. line between clusters). 
    * This is actually SVM.
    * Doesn't work good on hi-dim as most of the instances are very close to frontiers.
    * Then let's do forward selection: e.g. bring instances one by one. if instance is classified by other examples already, ignore it.
     
* Avoiding overfitting in k-NN:
  * simplest overfitting control parameter: k
    * big k: overfitting
    * finding best value of k: increase k on validation data (cross validation)
  * form prototypes - similar to above.
    * have big clusters --> less overfit
  * remove noisy instances
    * e.g. if all nearest neighbors have the same class different than the instance, then it is noise
    * more sophisticated ways are available - of course
    
#### Some types of instance based learning
* Locally weighted regression:
  * Don't do linear regression in advance
  * Do linear regression on nearest neighbors of new instance
  * Very cheap linear regression
  * This actually means we do piece-wise linear approximation to the curve (real function)
  * It will be slow on query time but not that slow since we do linear regression on k instances instead of millions
  * Quadratic or higher order regression is also possible
  
* Radial basis function networks
  * Global approximation to target function, in terms of linear combination of local approximations
  * Similar to locally weighted regression but eager instead of lazy
  * A different kind of neural network
    
* Case-based reasoning: a completely different instance based learning algorithm
  * Similar to help desks: this much RAM, this OS, ethernet connected; then the reason of the problem is XYZ
  * Distance measure: match qualitative function descriptions
  
* Collaborative filtering: AKA recommender systems
  * Predict if someone will like a website, movie etc.
  * Old approach: look at content of the website, movie etc. (is this an action movie etc.)
  * Collaborative filtering method:
    * Look at what similar users liked
    * Similar users == people with similar likes and dislikes
    * Rating prediction - parameters: (for movie M) 
      * user's average rating to movies
      * nearest neighbors' rating on M
      * nearest neighbors' average rating to movies
      * similarity to nearest neighbor --> this is calculated as *Pearson coefficient*
      * normalization

Statistical learning
==================================================================================================================

#### Bayesian learning

* Bayes' theorem: 
  
    P(h|D) = P(D|h) P(h)  /  P(D) 
             
                

  P(h)
  : prior probability of hypothesis h (e.g. you have cancer). 
  
  P(D)
  : prior prob of training data D (e.g. just previous experience = data)
  
  P(h|D)
  : prob of h given D
  
  P(D|h)
  : prob of D given h

  

#### MAP learners (optimal prediction)

  Maximum a priori
  : How much you believe in your hypothesis before you see any data?

  Maximum a posteriori
  : (MAP) How well your hypothesis go with the data? Pick the maximum matching one.                       


* Brute force MAP Hypothesis Learners:
  * Calculate the posterior probability of all Hs and pick the one that has highest posterior probability
  * Suffers from overfitting. To overcome that, one can make use of priori knowledge.


#### Bayes optimal classifier

* What happens when we received a new example to classify? 
  * Given I have 3 hypotheses with p's 0.4, 0.3 and 0.3
  * Tests against the h's are +,- and -
  * MAP Hypothesis says it is +, but probability of -'s are more
  * Correct class is -
* Bayes optimal classification is aware of this problem.
  * Test every hypothesis one by one and then basically find the most voted class. 
  * However, Bayes optimal classifiers are not practical at all because it requires too much computational power

* Gibbs Classifier
  * Pick a random hypothesis but more likely hypotheses should have more probability to be picked
  * Use that to classify the instance
  * In worst case, has 2x error rate of the Bayes optimal classifier 


#### Naive Bayes learner

* Very very naive thing. Just compute the product of the probabilities of (testExample|classValues). Pick the class that
  has max value.
* It just works very well as a classifier. Assumes things are independent, thus random
  * The output probability value cannot be trusted. It is unrealistically close to 1 or 0.
  * Basically, it just says, "here is the class that has the highest probability."
* What if one test example is not seen before? Multiplication with 0 will kill the product.
  * Use one of the smoothing techniques. Such as m-estimate
  

#### Example: text classification

* Plain old naive bayes learner reaches very high success rates. 
  * Examples: text being interesting or not, email being spam or not, text blongs to what news group


#### Bayesian networks

* Naive Bayes learners have big assumptions like things are independent
* Bayesian networks are developed to overcome this problem
  * Limited amount of dependencies are allowed
  * Probability of something is basically just dependent on parents (think of a graph)
* BTW, Bayesian networks are not just classifiers: it computes the conditional probability of any variables in it
  * However, inference is NP-hard
  * For that there are some methods like Monte Carlo methods
* Learning Bayesian Networks
  * Variants:
    * Network structure is known or not
    * Is there missing data or not
  * If structure is known and there is no missing data, it is es easy as training a Naive Bayes classifier
    * Then just look at the data and compute stuff
  * If there are missing values, then EM is the way


#### EM learning

* EM: Expectation Maximization
* A general algorithm; is not only applicable to Bayesian networks
* Solution for missing values in the training data
* Until convergence:
  * Fill the network by doing inference and computing expected values
  * Calculate new parameter values to maximize probability
* It basically finds the local optima. But, sometimes local optima is not the global optima. Then you have a poor solution.
  * Some notes for getting better results: 
    * Selecting the starting point is very important. 
    * Some people run the algorithm multiple times for different starting points.
  * You never know if your model is the best one (if your local optima is a global one)
  
#### Learning Bayesian Network Structure

* What happens when network structure is unknown?
* Structure search:
  * Start with an initial structure (empty network)
  * Add edges whenever you see data
  * ...
  * Maximum likelihood: vulnerable to overfitting
    * It will result in a completely connected network
  * Instead, use a prior which prefers smaller networks (less edges)
  * Or, draw the initial network manually if possible and then pass it to algorithm  

  
#### Structural EM algorithm

* What if there is missing values in training data and the network structure is unknown?
  * Naive idea: do EM and structure search at the same time.
  * Not efficient at all.
* Structural EM: Do the structure search inside the EM, not vice versa.
  * Deep thing!


Neural networks
==================================================================================================================

* Properties of a neural network:
  * Many neuron-like threshold switching units
  * Many weighted interconnections among units
  * Highly parallel, distributed process
  * Emphasis on tuning weights automatically: strength of connections tune automatically based on data


#### Perceptrons

* An old one.
* Simulate single neuron
  * x0 is always 1; it acts as a threshold
* Cannot learn everything. 
  * Can learn functions that have values linearly separable
  * Cannot learn, e.g. XOR function

* How to train a perceptron:
  * Just like a neuron: when you see something, the link (synapse) gets strengthened
  * However, it is error-driven. That means:
    * Don't mess with weights when there is no error; namely perceptron output and target value is the same
    * Do increase/decrease weights when there is an error
    
* Perceptron training rules:
  * The learning rate must be sufficiently small. Too big: you learn to quick but wrong. Too small: you learn very slow.
  * Training data must be linearly separable: **No noise allowed!** 
  

#### Gradient descent

* Widely used
* Finds the weights that minimizes the squared error 
  * Take the steepest step that minimizes the squared error
  * Go until the optimum: where all the neighbors increase the squared error

* Difference from perceptron:
  * Works with noise as well and even when the training data is not linearly separable
  * There is no black-or-white; there is a continuous signal in terms of neuron output

* Batch vs. incremental
  * Batch: wait until all data is seen to update weights
  * Incremental: update weights when an example is seen
  * Similar to learning at night(batch) vs. learning during the day(incremental)
  * Incremental is much faster.
  * Incremental way doesn't guarantee the global optimum, can be stuck in a local optimum.

#### Multilayer networks

* 

#### Backpropogation

* Most popular algorithm for learning neural networks
*




TODO:

* UWO MachLearning course
* Stanford MachLearning course
* Book: Algorithms of the Intelligent Web
* Book: Lucene
* Book: Lucene - SOLR, similar
* Book: Hadoop
* Book: Mahout
* Book: Apache Spark, MLib
* Try every single algorithm on Spark MLib
* Book: Apache OpenNLP
* Book: Scala
* Titanic example with Spark
* Other Kaggle projects

 

General stuff
==================================================================================================================

#### Some shared stuff

Gaussian distribution
: Normal distribution (the bell curve)




#### Probability estimates from small samples

* Need smoothing. Two of the possible methods:
    * Laplace estimate
    * General prior estimate

#### Lazy methods

Wait for query before generalizing:

* k-NN, case-based reasoning

#### Eager methods

Generalize before seeing query:

* ID3, FOIL, naive bayes, neural networks

#### Noise

* When you believe the noise is Gaussian, then minimizing the sum of squared errors is a good way of 
  evaluating hypotheses to find the best hypothesis (not sure if it only applies to linear functions) 

#### Math

* Never multiply probabilities. Log them and add them.


       
<style>
/** Some special overrides for this page **/
@media screen and (min-width: 1900px) {
    blockquote{
        color: inherit;
        font-style: inherit;
        letter-spacing:inherit;
    }

    dt{
        width: 350px;
    }

    dd{
        margin-left: 370px;
    }
}
</style>