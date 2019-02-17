---
layout: post
title:  "2018 Paper and Book Reading List"
date:   2018-12-09
excerpt: "especially if you're interested in fixed income and market microstructure..."
tag:
- Paper recommendation
---



2018 is coming to an end, and by the end of this year I picked up a new hobby - answering quesitons on stack exchange (more specifically on [quant fiance]( https://quant.stackexchange.com/)). It appears that a lot of times I see questions iterating over the same idea, and it made me wonder what if we can have a list of paper recommendations for anyone interested in quant finance, to start from the essentials and build a good foundation.  

So I decided to open this blog and share my reserves and interests with the folks. As a easy start, I will give a recommended reading list for understanding basics in some subfields of quant finance, and deeper digging in fixed income and market microstrucutre (I'm more focused on these).

You'll find in this article: 
1. Modern Portfolio Management
2. Execution
3. Fixed Income
4. Machine Learning - general
5. Market Making and Microstructure

**disclamer: I won't write recommendatin reason for all

## Modern portfolio management
1. Active Portfolio Management: A Quantitative Approach for Producing Superior Returns and Selecting Superior Money Managers.

**Reason**: If it is not THE book in this area. Was recommended by my professor Gordon Ritter (who recently won the buyside quant of the year, woah!!), for the class active portfolio management. Starting with CAPM, it goes deeper to how and what to attribute your return to. With this you'll have the foundation on how to use basic regression in your portfolio for performance. It is mathematically straightforward and very easy to follow (understanding of linear algebra is sufficient I'd say).

## Execution
1. [Execution strategies in fixed income markets](http://citeseerx.ist.psu.edu/viewdoc/download;jsessionid=3DF6A80EC589C258C238ACA68F065873?doi=10.1.1.421.4916&rep=rep1&type=pdf)
2. [Optimal execution of portfolio transactions](https://www.math.nyu.edu/faculty/chriss/optliq_f.pdf)
3. [Optimal Microstructure Trading with a Long-Term Utility Function](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3057570)

**Reason**: the first and second cover the 3rd generation foundation of optimal execution by Almgren, a must read. Third one is built upon on the previous and talks about maintaining neutrality while executing a market neutral portfolio.

## Fixed Income Trading:
Pricing related:
1. [Affine principal component term structure model](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2438623)
2. [A principal-component-based affine term structure model](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2451130)
3. [Three ways to solve for bond prices in the vasicek model](http://www.kurims.kyoto-u.ac.jp/EMIS/journals/HOA/JAMDS/8/11.pdf)

Trading in general:
1.  [A canonical analysis of multiple time series](http://pages.stern.nyu.edu/~dbackus/BCZ/HS/BoxTiao_canonical_Bio_77.pdf)
2.	[Pro-rata matching in one-tick markets](https://www.cass.city.ac.uk/__data/assets/pdf_file/0004/128083/Large.pdf)
3.	[Identifying small mean reverting portfolios](https://www.di.ens.fr/~aspremon/PDF/MeanRevVec.pdf)
4.	[Estimating the yield curve using the Nelson-Siegel model, a ridge regression approach](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2054689)
4.	[Stochastic permanent breaks](https://www.mitpressjournals.org/doi/abs/10.1162/003465399558382?journalCode=rest)

**Reason:** some of the basics on pricing futures and forwards, what's the most famous way to approximate PDE in fixed income pricing, and reducing colinearlity. In trading, fixed income sees a lot of pairs trading strategy so I think it's essential to understand how the market works, and what pairs trading originated from to what problems you need to pay attention to while implementing.

## Machine Learning – general:
1. Elements of statistical learning
2. [Comparison of three evoluntionary algorithms: GA, PSO, and DE](https://pdfs.semanticscholar.org/9d07/cb2ffec8f5b63d6a329dec5b88987776303e.pdf)
Market Making and Microstrucure:

**Reason:** I can't say enough how much I love the elements of statistical learning. Actually, whenever someone approaches me and asks what he/she should read as a intro to machine learning, I would recommend this right away if they have some quantitative background. Start with this book and stick only to it will save you tremendous amount of time going through meaningless, souless "machine learning" books that won't even tell you how to infer on your parameters.

## Market Making and Microstrucutre
1. [Market making via reinforcement learning](https://arxiv.org/abs/1804.04216)
2. [Cash Treasuries vs Futures on October 15, 2014](https://quantitativebrokers.com/wp-content/uploads/2017/05/Oct15-BTec1.pdf)
3. [A stochastic model for order book dynamics](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.139.1085&rep=rep1&type=pdf)
4. [Order book dynamics in liquid markets: limit theorems and diffusion approximations](https://arxiv.org/abs/1202.6412)
5. [The micro price: a high frequency estimator of future prices](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2970694)
6. [Clustering of order arrivals, price impact and trade path optimization](http://users.iems.northwestern.edu/~armbruster/2007msande444/Hewlett2006%20price%20impact.pdf)

**Reason:** Most of the researches are on limit order book structures, and are targeted at buy side firms who want to figure out what their sell sides are calculating. However in the similar way it can be applied in sell side, e.g. model your client's order arrival in a hawkes model!

That'd be all for now. 

---