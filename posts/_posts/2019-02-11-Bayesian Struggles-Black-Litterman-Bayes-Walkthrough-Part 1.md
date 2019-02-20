The beauty of mathematics, to me, lies the most in the ability of substantiating abstract ideas. One of my favorite to name is the orbit-stabilizer theorem (imaginable as a cube with orbit and you can flip it by rules).



The beauty of financial mathematics on the other hand, lies the most in everything comes down to a set of procedures all the time (uniformity!). For Black-Litterman optimization, it is falls under the category of statistical procedure, where we assume return follows a distribution, and portfolio managers' economics views are useful to infer the parameters of the distribution given our objective expectation.



Before we start, I want to acknowledge that everything I learned in this post was again, from my wonderful professor Gordon Ritter at his very amazing class Active Portfolio Management (I think available at NYU tandon and Baruch MFE program). This particular class was taken from his paper with Professor Petter Kolm (who I always see him being very excited about math details). Please read [their paper](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2853158) if you are interested in learning deeper (for example, the consideration on choosing prior)!  



### Intuitions on Black-Litterman-Bayes

Objective: find optimized holdings of our portfolio s.t.  $$h* = argmax_h {E[h'r] - \frac{{k}}{2}V[h'r] }$$

Translation: Need to estimate mean and variance of $$r$$ to solve mean-variance optimization

Elements needed:

- Unconditional expectation and variance of $$r$$ to get posterior update $$ r \sim  N(\theta,\sum)$$
- $$ r$$'s conjugate prior, let $$ \theta \sim N(\Pi,C)$$
- priori optimal portfolio holding $$ h_b$$



### Bayesian Set Up

Imagine we have some portfolios, and N portfolio managers has opinion on what sector might outperform all other sectors by a percentage, $$ q%$$. Then essentially the holdings on portfolio of each manager makes up a matrix $$ P$$ of N rows and each row is a set of holdings. Then our expected return on the whole portfolio equals to $$ q$$ . 

- on a detailed level, we have $$ E(p_ir) = q_i$$ for $$ q_i$$ in $$ \mathbb{R}$$

Importantly, we specify error for each expectation, for which we will denote as $$ \epsilon_i \sim N(0, \Omega)$$ and thus we have a likelihood to maximize. 

Our calculation steps then follow:

1. calculate posterior of $$ \theta$$, $$ p (\theta \lvert q) = \frac{f(q \lvert \theta)\pi(\theta) }{\int{f(q\lvert \theta)\pi(\theta)}}$$
2. use the above to calculate the posterior of $$r$$: $$ p(r \lvert q) = \int{p(r \lvert \theta)p(\theta \lvert q)d\theta} $$ 

3. use the mean and variance of posterior of r to calculate $$ h_{opt}$$



### Posterior of $\theta$

Very obviously we can approximate the posterior to $$ N(q \lvert p\theta,\Omega) N(\theta \lvert \Pi,\Omega)​$$ according to item 1. (question to readers, think about why are normalizer neglect-able?). 

Having normal distribution in hand, we realize that it's much easier to get log form and log function preserves monotonicity. Finally we have:
$$
\begin{align*} 
&\small -2logp(\theta) \sim (P\theta-q)'\Omega^{-1}(p\theta-q) + (\theta-\Pi)'C(\theta-\Pi)\\
& \small 	= please\ pick\ up\ your\ pen\ and\ multiply\ out\ the\ brackets \\
& \small	= \theta'(P'\Omega^{-1}P+C^{-1})\theta - 2(q'\Omega^{-1}P + \Pi'C^{-1})\theta \\
& \small = \theta'H\theta - 2\eta\theta \\
\end{align*}
$$



For simplicity, let $$ H = P'\Omega^{-1}P+C^{-1}$$ and $$ \eta = q'\Omega^{-1}P + \Pi'C^{-1}$$

Now, think about how we get mean and covariance of $$\theta$$
$$
\begin{aligned} 
& \small logp(\theta) \approx c + \frac{(\theta-\mu)^2}{\sigma^2}\\
& \small \approx \frac{\theta^2}{\sigma^2} + \frac{2\theta\mu}{\sigma^2}\ (omitting\ terms\ without\ \theta)\                  (4)
\end{aligned}
$$


It's then clear that $$ H = \frac{1}{\sigma^2}\ and\ \eta = \frac{\mu}{\sigma^2} $$ so we have covariance equals to $$ H^{-1}$$ and mean equals $$ H^{-1}\eta$$.



### Posterior of r

Well at this stage, I bet my readers already know the derivation for this one. Thanks to conjugate prior, we will be able to maintain the same update format as $$ \theta$$. 

let $$ \xi = H^{-1}\eta, v = H^{-1}$$, hence 
$$
\begin{aligned} \small p(r|q) \sim N(r|P\theta,\Omega) N(\theta|\xi,v)
\end{aligned}
$$


Similarly, we let $$H_r = V^{-1} + p'\Omega^{-1}P, \eta'_r =\xi'V^{-1} + r'\Omega^{-1}P$$, and one more term $$z = r'\Omega^{-1}r + \xi'V^{-1}\xi$$

and using the same trick, we get 
$$
\begin{aligned} 
& \small \mathbb{E}(r) = (\Omega^{-1}+\Omega^-1PH_r^{-1}P'\Omega^{-1})^{-1}\Omega^{-1}PH_r^{-1}V^{-1}\xi\\
& \small \mathbb{V}(r) = (\Omega^{-1}+\Omega^{-1}PH_r^{-1}P'\Omega^{-1})^{-1}
 \end{aligned}
$$



Recall our portfolio set up, we can now obtain optimal portfolio holding
$$
\begin{aligned} \small h_{opt} = (k\mathbb{V}(r))^{-1}\mathbb{E}(r)
\end{aligned}
$$



### End Note

Originally I imagined putting everything in one post, but while writing it I decided it's best to follow the structure of most generalized derivation -> introduction of arbitrage pricing theory model -> application, from dataset specs to code. So stay tuned for the following posts in this series! 
