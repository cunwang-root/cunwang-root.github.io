---
mathjax: true
---
## 1. Probability
test $$E = mc^2$$
goals of probabilistic inference
    1. parameter estimation
    2. given the parameters, what's the probability of the data
    3. is the model well-suited to the problem

types of queries
    1. probability queries  P(Y|E=e) = ?
    2. maximum a posteriori (MAP) queries   the highest probability joint
assignment to some subsets of variables.
    
## 2. Directed Graphical Models
DGMs are also known as Bayesian networks.

A clique is a set of nodes where every pair of nodes is connected by an
edge. A maximal clique is the one that loses the clique property if it
includes any other node.

the independence assumptions in the Bayesian network helps us avoid
specifying the joint distribution.

The modular structure of the Bayes network is the set of local probability
models that represent the nature of the dependence of each variable on its
parents. A CPD specifies a distribution over a random variable, given all
the combinations of assignments to its parents. Thus, the modular
 representation for a given Bayes network is the set of CPDs for each random
 variable.

Reasoning Patterns
    1. causal reasoning     
    2. evidential reasoning
    3. inter-causal reasoning

D-separation
A trail is active if it contains no V-structures, in the event that no
evidence is observed.

Factorization and I-maps (Independency map)

The Naive Bayes model is the one that makes simplistic independence
assumptions.

## 3. Undirected Graphical Models
pairwise markov network

We can define a pairwise Markov network as an undirected graph composed of
nodes that represent random variables, which are connected by edges between
two nodes.

the gibbs distribution

each factor might have several variables in its scope, and the gibbs
distribution is a set of such factors.

Factorization

One way to understand factorization is to think of it as a decomposition 
problem. Different sets of factors can induce the same graph, and the 
factorization, or splitting into individual factors, cannot be read from the
graph. 

Flow of influence

Two variables can influence each other as long as they are connected through
a set of edges.

Active trail and separation

the rule is simple: an influence can flow between any two random variables 
that are connected by edges. A node is blocked if it has been observed.
The random variables X and Y, given the evidence set Z, are separated in a 
graph G if there is no active trail in G between X and Y. 

Structured prediction

there are several classes of applications where the target variable is 
related to its neighbors. In such cases, where we wish to perform 
task-specific prediction, and there exists a local structure that we can 
exploit, we can use models such as Hidden Markov Models (HMMs) and 
Conditional Random Fields (CRFs).

The CRF representation
A CRF seems similar to the Gibbs distribution. The difference is that the 
normalization constant Z only sums over all the values of Y.

## 4. Structure Learning
When we wish to use a PGM, one task is to determine the structure of the 
graphical model. Sometimes, we have a domain expert who can arrange a 
suitable hierarchical model. Unfortunately, this is not always the case, 
and we may want to learn the structure of the network given the data without
any prior domain knowledge. Even with some domain expertise available, we 
would like to verify or improve the structure of the network.

Another use of structure learning is when the goal is to discover the 
structure (and not necessarily discover it just to run inference queries). 
For example, causal Bayesian networks have been used to model protein 
signaling networks, where discovering the network structure is applied to 
understand drug interactions and dysfunctional signaling in diseased cells.

### The structure learning landscape
the algorithms that we discuss can be divided into two areas, one that uses
constraints and the other that focuses on score-based approaches.

We will also discuss the kind of structures that are found, such as trees, 
forests, and graphs.
