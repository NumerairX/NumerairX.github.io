---
layout: post
title:  "Bayesian Struggles: why we need conjugate priors"
date:   2018-12-22
excerpt: "starting with two simple examples..."
tag:
- statistics
---

I want to start this first post of the series of Bayesian stats with this meme.

<a href="{{ site.url }}/assets/img/blog/bayesfun.png"><img src="{{ site.url }}/assets/img/blog/bayesfun.png" alt="bayesian meme"></a> 

(image from [Bayesian Fun](https://www2.isye.gatech.edu/~brani/isyebayes/jokes.html))

It is also important to make sure my dear reader(s) knows that I am by all means not an expert in statistics (let me know if u found mistakes!). I came from an applied math background but had no interest in taking stats in college (thought it was easy and too formulaic at that time, naive!!). So I am almost completely self-taught in this subject and prone to interpret things in a familiar way to help me understand. 

However, I  think because I had (a lot of) struggles, I can share better how the logic flows to overcome them.



### How did we come to realize that we might need something called conjugate prior?

Consider the example given by Bayes himself in his 1763 paper: let us roll a ball along unit interval $$[0,1]$$ with uniform probability of stopping anywhere in between. 
This ball finally stopped at distance $$\theta$$ and we then throw this ball for $$n$$ times. Denote the number of times ball stops before reaching 
$$\theta$$ as $$x$$, what can we learn about $$\theta$$ now (aka what is $$p(\theta|x)$$)?

In this case our prior is no longer just our *'belief'* but a physics fact. We understand that $$p(\theta)$$ is 1 since it follows uniform distribution, 
and $$p(x|\theta)$$ is just binomial probability density function.

$$p(x|\theta)=$$
$$           \int_{0}^{1}\theta^x(1-\theta)^{n-x}d\theta$$ 

$$           =\frac{1^{k+1}(1-1)^{n-k}}{k+1}-\frac{0^{k+1}(1-0)^{n-k}}{k+1}$$

$$             +\frac{n-k}{k+1}\int_0^1 p^{k+1}(1-p)^{n-k-1}$$	 

$$           =  ...$$ keep doing integration by parts

$$           = \frac{x!(n-x)!}{(n+1)!}$$



which verifies to be beta distribution of $$\alpha = x+1, \beta = n-x+1$$.

With all the elements known, by Baye's theorem $$p(\theta|x) \propto p(x|\theta)p(\theta) $$, our posterior follows beta distribution of the above parameters.
However, if instead we take $$Beta(\alpha,\beta)$$ as our prior, our posterior then follows:
$$p(x|\theta)p(\theta) \propto \theta^x(1-\theta)^{n-x}\theta^{\alpha-1}(1-\theta)^{\beta-1} \sim Beta(\alpha+x,\beta+n-x)$$.



*highlight*:

1. our posterior has the same form as prior which makes it easy to update

2. prior now also have explanation power: 

   while we roll the ball, each time it stops before $$\theta$$, it corresponds to the probability density of binomial as in increase of successful trail (aka $$x+1$$),
   so imagine if we were live-recording the rolling, we would add 1 to $$\alpha$$.  If it exceeds the line, we would add 1 to $$\beta$$.  Very intuitive.



#### Did that really make much of a difference? Yes if we bring complicated integrals in the house!

let's imagine a slightly more complicated case, where you are trying to infer the parameters of your dataset, which you believe to follow normal distribution. 
You don't get nice property like $$p(\theta)$$ just equals to 1 and needs to do  
$$\int_{- \infty}^{\infty} \frac{1}{\sqrt{2\pi\sigma_0^2}} e^{\frac{-(\mu-\mu_0)^2}{2\sigma_0^2}} * \frac{1}{\sqrt{2\pi\sigma^2}} e^{\frac{-(x-\mu)^2}{2\sigma^2}} d\mu$$
 every time you update. This is actually why most times we want find nice conjugate priors to avoid computing high dimensional integration. The benefits will came clear after the below explanation.



> Consider i.i.d sample $$X = (x_1,x_2, ..., x_n)$$ are drawn from distribution  $$N(\mu,\sigma^2)$$ with **$$\mu$$ and $$\sigma^2$$ random**. Let $$\tau = \frac{1}{\sigma^2}$$, it is suffice to have parameter set $$\theta = (\mu, \tau)$$. 

#### Our goal: find $p(x|\mu,\tau)$

    Tricky part: find $$p(\mu,\tau)$$

Similarly to the problem of only $$\sigma^2$$ fixed, consider a gamma prior, $$\tau \propto \Gamma(\alpha,\beta) $$, and we use the parametrization that PDF is $$ \frac{\beta^\alpha}{\Gamma(\alpha)} x^{\alpha-1} e^{-x\beta}$$ then for $$\sigma^2$$ is (obviously) an inverse gamma distribution, aka $$\sigma^2 \propto IG(\alpha,\beta)$$.

However, I did struggle a while understanding what $$\mu$$ should be because it seems independent of $$\sigma^2$$. 
But if $$\mu$$ and $$\sigma^2$$ are independent of each other, posterior won't be in inverse gamma format so we end up having nothing handy. 
Later from the wisdom of my professor, he made that $$\mu|\tau \propto N(v, \frac{1}{k\tau})$$ for $$v, k$$ being some real number and of course $$k>0$$. 
The reason behind is given both conditioned on $$X$$ , $$\mu$$ and $$\sigma^2$$ should be dependent. 

The full prior density $$p(\tau,\mu)$$ is then $$p(\tau)p(\mu|\tau)$$
$$ = \frac{\beta^\alpha}{\Gamma(\alpha)} x^{\alpha-1} e^{(-x\beta)} \sqrt{\frac{k\tau}{2\pi}} e^{({-\frac{k\tau}{2}(\mu-v)^2})}$$ **(1)**

and posterior $$p(\mu,\tau|x)$$
​           = *(1)* x $$(\frac{\tau}{2\pi})^{\frac{n}{2}}e^{({\frac{-\tau}{2}}\sum_{i}(x_i-\mu)^2)}$$

Omitting some merging and substituting tricks that nobody wants to see, we come down to $$p(\mu,\tau|x)​$$
$$\propto\tau^{\alpha'-1/2}e^{(-\tau(\beta' + \frac{k'}{2}(\mu-v')^2))}​$$

$$\alpha' = \alpha + \frac{n}{2}$$

$$\beta' = \beta + \frac{1}{2} \frac{nk}{n+k}(\bar{x}-v)^2 + \frac{1}{2} \sum_{i} (x_i-x)^2$$

$$k' = k+n'$$

$$v' = \frac{kv+n\bar{x}}{k+n}$$

leaves only four simple algebra to maintain at each update.


To end this article, I will share a fun read, [A Catalog of Noninformative Priors](http://www.stats.org.uk/priors/noninformative/YangBerger1998.pdf) I found a while ago. 
