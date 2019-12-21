As it's approaching the end of 2019, I want to review what I have learned this year, and again share my reading list. Around June, I asked myself what are the foundations a good junior level strat/quant should have, to be at least able to understand and critic existing academic papers or algorithms and come up with something on his/her own. I decided on the follow, and lease leave a comment if you think I missed anything!

- **Statistical Sense:** Know how to do hypothesis testing correctly; know how to test significance properly; know the origins of each distribution (family); understand assumptions in fitting distributions; understand when to and when not to be independent; clear on trade offs between error types; understand how bias and variance arise with different models and aggregation methods; understand Bayesian statistics;  know what led to use of M-estimator and why it's used; understand stochastic calculus concepts, drift, jump, hitting time, exact solution and approximation;
- **Time Series and Econometric:** understand how to model time series (very broad); know back-shift operators and when convergence is guaranteed; Understand the mathematics of stationarity; Understand order of integration and cointegration; ACF and PACF, how to interpret the graph, and use to choose order in ARMA; Metrics for evaluating econometrics forecasts; 
- **Numerical Methods:** know the complexities of major linear algebra operations and how to derive; know some ways to speed up computation; understand Monte Carlo and Las Vegas algorithm (should this be under this category?); linear and non linear programming; trade offs between different optimization algorithms;
- **Combinatorics:** understand how to reduce problems to base case and solve by recursion; understand how to interpret problems in combinatorics sense to reduce counting;  

I tried to expand my knowledge base in each categories, but for the first two I learned an extreme amount  from designing my first ever quant strategy at work (has been up and running in production for four months now!). Kudos to countless mathematics exchanges and cross validated answers, and to all stack exchange communities! Now moving on to the books I've read this year. I have mostly focused on optimal control since I have been interested in learning it systematically for quite long. There are some particular things I look for when picking one to be my main source: 

1. must be math-centric. I avoid any books titled "with python/R applications"  

2. preferably an "old" book in the field
3. Fun to read, some but not excessive examples 
4. On par with undergraduate level textbook standard

### The Topics

1. ##### convex optimizations (recommend Convex Optimization by Stephen Boyd)

   Understand quadratic programming, types of ways to solve it, types of ways to relax constraints. The book recommended is very easy to follow and should be a quick read, I suggest check out the Algorithms part first to see how much you already know.

2. ##### dynamic programming (recommend Introduction to stochastic Dynamic Programming)

   To understand how to correctly apply reinforcement learning, one must first understand Markov decision process (the problem), then the basics of dynamic programming (the solution; back tracking, approximation, optimality principal in discrete and continuous setting).

3. ##### Reinforcement Learning (recommend Reinforcement Learning by Richard Sutton)

   Now, I had extreme fun reading and doing problems in Sheldon Ross's book. This one by Richard Sutton provides you some overlaps, but gives very structured advices from on policy to off policy, tabular to approximation (faster and more room to integrate with other machine learning algos), 1 step to n-step (which will be helpful in understanding experience replay). Only things I wish this book would've had is more mathematical details.

   I have implemented a bot utilizing various RL algos for my current work, the fun to effort ratio is very good so I highly recommend you to formulate a problem on your own, code it up and plug in some data! Later you will see there are so many niches to improve, and that will drive more researches.

4. ##### Elements of Statistical Learning

     I start looking at it for the third time, and I think I am still getting information out of it.

5. ##### Tricks in Machine Learning (recommend Advances in Financial Machine Learning by Marco Lopez De Prado)

   Very fun and easy read by the time you have had all the basics of applying statistics in building your quantitative strategies. Now it's the time to listen to what Marco has to say about the mistakes you might have been making (from my junior level point of view). 

    Are you modeling your input time series wrong? Are you applying cross validation wrong? Are you assuming your inputs' distribution are independent? Are you considering all metrics you should consider during backtests? Find answers to all in this book. Take it with a grain of salt reading any book of this kind, and don't resort to it as a magic potion (I once interviewed a more senior candidate who told me his strategy was "code snippet" from Marco's book).

6. ##### Random Matrix Theories (no book recommendation)

   Often you will need to estimate a very sparse covariance matrix, RMT can be applied here and for some cases we could guarantee recovery of largest eigenvalue. One paper that really helped me is [Random Matrix Theory and its Innovative Applications by Alan Edelman and Yuyang Wang](http://math.mit.edu/~edelman/publications/random_matrix_theory_innovative.pdf). But one should go Google more sources to answer any questions arise.

   

   

   

   