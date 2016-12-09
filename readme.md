##Content Overview/Important Concepts
More detailed info and reading can be found in the repo subdirectories

### Wiki Study Guide
http://wiki.omscs.org/confluence/display/CS7641ML/CS7641.FA14.+Final+exam+prep

###Unsupervised Learning
UL consists of algorithms that are meant to "explore" on their own and provide
the user with valuable information concerning their dataset/problem

* Randomized Optimization
* Clustering
  * Single Linkage
    * Consider each of n points a cluster
    * Find the distance between the closest two points in every cluster
    * Merge the closest two clusters
    * Repeat n - k times to get k clusters
    * Method:
      1. Consider each point a cluster
      2. Merge two closest clusters
      3. Unless we have K clusters GOTO 2
    * Links points closest to each other.
    * Can result in "stringy" non-compact clusters
    * Terminates faster than KM and EM
    * It is deterministic
    * Complexity of O(n3)
    
  * K-Means
    * Each iteration is polynomial O(kn)
    * Finite (exponential) iterations in theory, but usually much less in practice O(k^n)
    * Error decreases if we break ties consistently hence it ALWAYS converges
    * Can get stuck with "weird" clusters depending on random starting state
      1. Place k centers randomly
      2. Each center claim closest points
      3. find the centers of the points
      4. Move the centers to the clusters of points
      5. Unless converged GOTO 2
    * Center may not be a point on the cluster
    * Produces more compact clusters
    
  * K-Means as optimization
    * Confiugrations or inputs can be scored and we need configurations with high score
    * Score is the sum of all the squared distance between a point and its cluster 
    * Why does it converges
      1. Finite number of configurations, objects and labels and hence center is constrained
      2. Break ties consistenly
      3. Never go into configuration of higher error

  * Soft Clustering
    * Allow for points to be shared across clusters
    * Find hypothesis that maximises the probability of data.
      1. Select one of k Gaussians
      2. Sample X from that Gaussian
      3. Repeat n times
    * Maximum likelihood mean of Gaussian is the mean of the data
    
  * Expectation Maximization
    * Gaussian Means
    * Uses expectation and maximization steps
    * Monotonically non-decreasing likelihood
    * Does not converge (practically does) because of probability
    * Can get stuck
    * Works with any distribution (not just Gaussian)
    
  * Properties of Clustering Algorithms (Pick 2)
    * Richness
    * Scale Invariance
    * Consistency
    
  * Richness
    * For any assignment of objects to clusters, there is some distance matrix, D,
      such that P_D returns that clustering
  * Scale-Invariance
    * Scaling distances by a positive value does not change the clustering
  * Consistency
    * Shrinking intra-cluster distances and expanding intercluster distances does
      not change the clustering.
  * **No clustering scheme can acheive all of Richness, Scale-Invariance, Consistency**

* Feature Selection
  * Filtering
    * Choose features independent of learner. i.e. "filter" the data before it
      is passed to the learner
    * Faster than wrapping (don't have to pay the cost of the learner)
    * Tends to ignore relationships between features
    * Decision Trees do this naturally (Filter on information gain)
  * Wrapping
    * "Wrap" the learner into the feature selection.  Choose features based on
      how the learner performs.
    * Takes into account learner bias
    * Good at determining feature relationships (as they pertain to the success
      of the learner)
    * Very slow (have to run the learner for each feature search)
    * Speed Ups
      * Randomized optimization
      * Forward/Backward sequential selection: [good description and
        implementation](http://sebastianraschka.com/Articles/2014_sequential_sel_algos.html)
  * Relevance
    * ![x_i](http://mathurl.com/2az2c7m.png) is strongly relevant if removing it degrades the Bayes' Optimal
      Classifier
    * ![x_i](http://mathurl.com/2az2c7m.png) is weakly relevant if
      * it is not strongly relevant
      * ![There exists](http://mathurl.com/yhy6gla.png) a subset of features **S** such that adding             ![x_i](http://mathurl.com/2az2c7m.png) to **S** improves Bayes' Optimal Classifier
      * ![x_i](http://mathurl.com/2az2c7m.png)  is otherwise irrelevant
  * Relevance vs. Usefulness
    * **Relevance** measures the effect the variable has on the Bayes' Optimal
      Classifier
    * **Usefulness** measures the effect the variable has on the _error_ of a
      _particular predictor_ (ANN, DT, etc.)

* Feature Transformation
  * Polsemy: Same word different meaning - False Positives
  * Synonomy: Different word same meaning - False Negatives
  * PCA: [Good Slides](http://www.cc.gatech.edu/~agray/4245fall10/lecture18.pdf)
    * Example of an eigenproblem
    * Finds direction (eigenvectors) of **maximum variance**
    * All principal components (eigenvectors) are mutually orthogonal
    * Reconstructing data from the principal components is proven to have the
      least possible L2 (squared) error compared to any other reduction
    * Eigenvalues are monotonically non-increasing and are proportional to
      variance along each principal component (eigenvector). **Eigenvalue of 0
      implies zero variance which means the corresponding principal component
      is irrelevant**
    * Finds **"globally"** varying features (image brightness, saturation, etc.)
    * Fast algorithms available
  * ICA
    * Finds new features that are completely **independent** (from each other).
      i.e. they share no mutual information
    * Attempts to maximize the mutual information between the **original**
      and **transformed** data.  This allows original data to be reconstructed
      fairly easily from the transformed data.
    * Blind Source Separation (Cocktail Party Problem)
    * Finds **"locally"** varying features (image edges, facial features)
  * RCA
    * Generates random directions
    * It works! If you want to use it to preprocess classification data...
        * Is able to capture correlations between data, but in order for this to
          be true, you must often reduce to a larger number of components than
          with PCA or ICA.
    * Can't really reconstruct the original data well.
    * Biggest advantage is speed.
  * LDA
    * Requires data labels
    * Finds projections that discriminate based on the labels. i.e. separates
      data based on class.

* Information Theory
  * Entropy: [A characterization of uncertainty about a source of    information](http://en.wikipedia.org/wiki/Entropy_(information_theory))
    * ![Entropy Formula](http://mathurl.com/pdmz66k.png)
  * Joint Entropy: [The entropy contained by the combination of two variables](http://en.wikipedia.org/wiki/Joint_entropy)
    * ![Joint Entropy Formula](http://mathurl.com/l3t2ekl.png)
  * Conditional Entropy: [The entropy of one variable, given another](http://en.wikipedia.org/wiki/Conditional_entropy)
    * ![Conditional Entropy Formula](http://mathurl.com/pvq7nq4.png)
  * Mutual Information: [The reduction of entropy of a variable, given knowledge of another variable](http://en.wikipedia.org/wiki/Mutual_information)
    * ![Mutual Info Formula](http://mathurl.com/o7es4gh.png)
  * KL Divergence: [A non-symmetric measure of the difference between two probability distributions P and Q](http://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence)
    * ![KL Divergence Equation](http://mathurl.com/kld5umv.png)
    * Can be used in supervised learning as an alternative to squared error


###Reinforcement Learning

[Reinforcement Learning: A Survey](http://www.jair.org/media/301/live-301-1562-jair.pdf)

Put an agent into a world (make sure you can describe it with an MDP!), give him
some rewards and penalties and hopefully he will learn.

* **Markov Decision Processes**
  * Building a MDP
    * States
      * MDP should contain all states that an agent could be in.
    * Actions
      * All actions an agent can perform.  Sometimes this is a function of state,
        but more often it is a list of actions that could be performed in any state
    * Transitions (model)
      * Probability that the agent will arrive in a new state, given that it takes
        a certain action in its current state: P(s'|s, a)
    * Rewards
      * Easiest to think about as a function of state (i.e. when the agent is in a
        state it receives a reward).  However, it is often a function of a
        [s, a] tuple or a [s, a, s'] tuple.
    * Policy
      * A list that contains the action that should be taken by the agent in each
        state.
      * The **optimal policy** is the policy that maximizes the agent's long
        term expected reward.
  * Utility
    * The utility of a state is the reward at that state plus all the (discounted)
      reward that will be received from that state to infinity.
    * Accounts for _delayed_ reward
    * Described by the Bellman Equation
      * ![Bellman Equation](http://mathurl.com/oj75ljf.png)
  * Value Iteration
      * "Solve" (iteratively until convergence, more like hill climb) Bellman
        Equation.
      * When we have maximum utility, the policy which yields that utility can
        be found in a straightforward manner.
  * Policy Iteration
      * Start with random (or not) initial policy.
      * Evaluate the utility of that policy.
      * Update policy (in a hill climbing-ish way) to the neighboring policy that
        maximizes the expected utility.
  * Discount Factor, ![gamma](http://mathurl.com/pbhmxd.png) (typically between 0 and 1),
    describes the value placed on future reward.  The higher ![gamma](http://mathurl.com/pbhmxd.png) is,
    the more emphasis is placed on future reward.

* **Model-Based vs. Model-Free**
  * Model-Based requires knowledge of transition probabilities and rewards
    * Policy Iteration
    * Value Iteration
  * Model-Free gets thrown into the world and learns the model on its own based
    on "[s, a, s', r]" tuples.
    * Q Learning
* Three types of RL
  * Policy Search - direct use, indirect learning
  * Value function based - ^Argmax
  * Model based - indirect use, direct learning ^Solve Bellman

* **Q Learning**
  * Q Function is a modification of the Bellman Equation
    * ![Q Function](http://mathurl.com/khys58v.png)
    * ![U(s)](http://mathurl.com/o8lnnnk.png)
    * ![Pi(s)](http://mathurl.com/pnfz5z6.png)
  * Learning Rate, ![alpha](http://mathurl.com/827tag.png), is how far we move
    each iteration.
  * If each action is executed in each state an infinite number of times on an
    infinite run and ![alpha](http://mathurl.com/827tag.png) is decayed appropriately, the Q values will converge with probability 1 to Q*
  * Exploration vs Exploitation
    * Epsilon Greedy Exploration
      * Search randomly with some decaying probability like
        Simulated Annealing
    * Can use starting value of Q function as a sort of exploration

* **Game Theory**
  * [**Zero Sum Games**](http://en.wikipedia.org/wiki/Zero-sum_game)
    * A mathematical representation of a situation in which each participant's
      gain (or loss) of utility is exactly balanced by the losses (or gains)
      of the utility of the other participant(s).
  * **Perfect Information Game**
    * All agents know the states of other agents
    * minimax == maximin
  * **Hidden Information Game**
    * Some information regarding the state of a given agent is not know by the
      other agent(s)
    * minimax != maximin
  * [**Pure Strategies**](http://en.wikipedia.org/wiki/Strategy_%28game_theory%29#Pure_and_mixed_strategies)
  * [**Mixed Strategies**](http://en.wikipedia.org/wiki/Strategy_%28game_theory%29#Pure_and_mixed_strategies)
  * [**Nash Equilibrium**](http://en.wikipedia.org/wiki/Nash_equilibrium)
    * No player has anything to gain by changing only their own strategy.
  * Repeated Game Strategies
    * Finding best response against a repeated game finite-state strategy is
      the same as solving a MDP
    * Tit-for-tat
      * Start with cooperation for first game, copy opponent's strategy (from the
        previous game) every game thereafter.
    * Grim Trigger
      * Cooperates until opponent defects, then defects forever
    * Pavlov
        * Cooperate if opponent agreed with your move, defect otherwise
        * **Only strategy shown that is subgame perfect**
  * Folk Theorem: Any feasible payoff profile that strictly dominates the
    minmax/security level profile can be realized as a Nash equilibrium payoff
    profile, with sufficiently large discount factor.
    * In repeated games, the possibility of retaliation opens the
      door for cooperation.
    * Feasible Region
      * The region of possible average payoffs for some joint strategy
    * MinMax Profile
      * A pair of payoffs (one for each player), that represent the payoffs that
        can be achieved by a player defending itself from a malicious adversary.
    * Subgame Perfect
        * Always best response independent of history
    * Plausible Threats
  * **Zero Sum Stochastic Games**
    * Value Iteration works!
    * Minimax-Q converges
    * Unique solution to Q*
    * Policies can be computed independently
    * Update efficient
    * Q functions sufficient to specify policy
  * **General Sum Stochastic Games**
    * Value Iteration _doesn't_ work
    * Minimax-Q _doesn't_ converge
    * _No_ unique solution to Q*
    * Policies _cannot_ be computed independently
    * Update _not_ efficient
    * Q functions _not_ sufficient to specify policy
