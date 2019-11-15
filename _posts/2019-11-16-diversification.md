---
author:
- Sturm Mabie
category: Posts
date: '2019-11-16'
mathjax: true
startup: showeverything
title: 'Diversification, Risk and Leverage'
---

Introduction
------------

In this stand-alone post, we will expound upon the concepts of and the
relationship between diversification, risk, and leverage. First, we will
dive into the concept of diversification and risk and then into the
interplay with leverage.

Background
----------

Diversification, the process of investing in many (ideally) uncorrelated
return streams, has been a strategy used to reduce risk for over
thousands of years. Diversification is mentioned in both the Bible and
the Talmud and came to prominence under the Roman Empire, when investors
would form investment partnerships for particularly risky business, such
as financing the voyage of a merchant vessel. While the original purpose
of these partnerships was to provide lucrative investment vehicles for
investors without enough capital to fund a voyage alone, they quickly
became popular for even the richest Romans who would often buy shares of
many different voyages simultaneously in order to diversify the large
risk of any single voyage.

The modern concept of diversification was popularized by Harry Markowitz
in the 1950s through his concept of a *Markowitz-efficient portfolio*
(MEP) and *Modern Portfolio Theory* (MPT). A ME portfolio is the
portfolio that lowers the portfolio\'s volatility through
diversification for a given level of expected return. Or in other words,
the portfolio that contains the most number of return streams that
maximize the return of the portfolio. MPT and MEP were the first
formalizations of diversification put forth, creating a framework for
viewing the character of a portfolio through the return and volatility
of the portfolio. Using the example of a discretionary equity investor,
the ME portfolio would consist of as many stocks as the investor could
find or research that would pass his investment criteria. Once the
investor starts adding less desirable stocks (stocks with a lower
expected return) that culminate in a portfolio with lower return than
the desired or expected return, he no longer holds a ME portfolio.

Later with the advent of the *Capital Asset Pricing Model* (CAPM) and
multi-factor models, the concept of risk became partitioned into two
primary categories: systematic risk and specific risk. While specific
risk can easily be diversified away by holding a ME portfolio,
systematic risk cannot. In the original formulation of CAPM, specific
risk was assumed to be zero and dropped from the equation:

$$r_i - r_f = r_f + \beta_i (r_m - r_f)$$

Where $\beta_i$ is $\rho_{i,m} \frac{\sigma_i}{\sigma_m}$, $r_f$ the
risk-free rate, $r_i$ the return of the asset $i$, and $r_m$ the
expected return of the market. The introduction of CAPM by William
Sharpe and others was a pivotal step in quantifying risk. In CAPM, a
portfolio\'s risk is defined as some multiple of the market\'s risk,
generally assumed to be the volatility of the market. This important
idea is best visualized by the Security Market Line (CML):

![Capital Market Line](/assets/sml.png)

While investors under the CAPM model can choose where on the line best
fulfills their investment goals ($\beta$), they are not able to easily
diversify away their market risk, as the *Efficient Market Hypothesis*
is going to push both undervalued and overvalued stocks toward the line
through arbitrage; nor can investors capture excess returns relative to
the systematic or market risk for the same reason. In it\'s essence,
CAPM posits that investors are compensated in returns in the exact same
proportion to the risk assumed. While this is not strictly true for a
compounding portfolio because of volatility drag (see my other post
[(1))](https://smabie.github.io/posts/2019/10/04/vol.html), this reveals
an interesting property of specific risk. Since specific risk can easily
be hedged against through the construction of a ME portfolio, investors
are only compensated for systematic or market risk, not specific risk.
Another consequence is that investors are more likely to view an asset
through it\'s systematic risk versus it\'s specific risk: an investment
with low sensitivity to the market but high specific risk may be judged
to have much less risk than a naive observer might expect.

In the next section, we will look at the mathematics of diversification
and uncorrelated random variables.

Portfolio Variance and Diversification
--------------------------------------

An interesting property of diversification is that mathematically
speaking, with every new security we add to our portfolio, the
volatility of the portfolio monotonically decreases. Let\'s define a
portfolio $Y$ that is a linear combination of two variables (assets):

$$P = aX_A + bX_B$$

Where $a$ and $b$ are the proportion or weights of the assets in the
portfolio. While the returns of the portfolio are a linear combination
of the two return streams of the assets, the variance is:

\\begin{align\*} *σ*~P~^2^ &= x~A~^2^ Cov(r~A~,r~a~) +
x~B~^2^Cov(r~B~,r~B~) + 2x~AxB~Cov(r~A~,r~B~)\
&= x~A~^2^ *σ*~A~^2^ + x~B~^2^ *σ*~B~^2^ + 2ab*ρ*~AB~*σ*~A~*σ*~B~\
\\end{align}

While not immediately obvious, the variance of the portfolio will always
be lower the more assets we add, as long as the no asset has a
correlation of 1 to any other asset. Since the equation starts to become
unwieldy the more assets we add to the portfolio, we often instead
represent the variance of a portfolio using matrices. Using the same
example of two assets $A$ and $B$, we first define the covariance
matrix:

$$\textbf{P}=\begin{bmatrix}
   \text{Cov}(r_A,r_A) & \text{Cov}(r_A,r_B) \\
   \text{Cov}(r_B,r_A) & \text{Cov}(r_B,r_B)
   \end{bmatrix}$$

Next we define our vector weights or proportions:

$$\textbf{x}=
   \begin{bmatrix}
   x_A \\
   x_B 
   \end{bmatrix}$$

Now we can define our variance in terms of the covariance matrix and the
vector weights:

$$\sigma_P^2 = \mathbf{x}^T\mathbf{Px}$$

This is often called the quad or quadratic form of $\mathbf{x}$ and
$\mathbf{P}$.

If the weights of all the assets are the same and they all have the same
variance, the standard deviation of the portfolio can be succinctly
found to be:

$$\sigma_P = \frac{\sigma}{\sqrt{n}}$$

Looking at the chart below, we can say see volatility first decreases
very quickly with increasing diversification but rapidly becomes more
and more marginal:

![Volatility vs Number of Assets](/assets/sqrtdev.png)

It now becomes even more clear why investors are not compensated for
bearing specific risk: it is incredibly easy to reduce most specific
risk with a relatively small number of assets. For equities in
particular the volatility cannot be reduced as much as the above chart
implies since most equities are highly correlated to each other through
their common systematic risk factors. Even so, as we will see in the
next section, we can get most of the way there with only 20-30 different
correlated assets.

In the next section, we will look at some market data and run some
simulations in order to better understand the affect of diversification
on a theoretical portfolio under real market conditions.

Diversification and Historical S&P 500 Returns
----------------------------------------------

In order to see how diversification affects volatility and returns in a
real environment, we ran a Monte Carlo simulation that generates 1000
random portfolios that longs $n$ number of random stocks, where $n$ is
all even numbers between 2 and 100, inclusively. All the stocks are
chosen from the S&P 500 and the daily portfolio returns are constructed
between 2017-01-01 and 2019-01-01. Below is a graph of average
annualized volatility and return as a function of assets held:

![Volatility and Return as a Function of Number of
Assets](/assets/div.png)

While the average annualized return does not change in any meaningful
way, the average annualized volatility looks very similar to the
previous graph of perfectly uncorrelated assets all sharing the same
volatility. Since we are picking stocks randomly, it is unsurprising
that we trend toward the ME portfolio with the same expected level of
return. While not shown in the graph, the average annualized volatility
of our portfolio trends quickly toward the annualized volatility of the
S&P 500 during the same period.

Leverage
--------

Though the aforementioned graph seems to imply that the volatility and
the return of our portfolio are orthogonal to each other, in reality,
for a compounding portfolio, this is not actually the case. due to the
mathematical nature of compounding returns and geometric sums, the
volatility of our portfolio has a very real affect on our long-term
returns. This phenomenon is coined *volatility drag* and increasingly
penalizes portfolios with higher and higher volatility. Conversely, the
lower our volatility the higher our expected compounded returns should
be. Below is the equation for volatility drag:

$$r_a = r_p - \frac{\sigma^2_p}{2}$$

Where $\sigma_p$ is the standard deviation of the portfolio, $r_p$ the
return of the portfolio and $r_a$ the actualized return of the portfolio
after accounting for volatility drag (for a more in-depth dive into
volatility drag
[(1)](https://smabie.github.io/posts/2019/10/04/vol.html)). Volatility
drag implies that not only should aim to reduce volatility for the
classically given reasons, but that reducing volatility actually lets us
boost our returns, which means that diversification provides even more
benefit than we might otherwise think.

Leverage and Diversification
----------------------------

A key result in the above linked post is the relationship between
volatility, return, and leverage. After a little bit of math we arrived
at the conclusion that in order to maximize our return, we should lever
up our investments as per the following equation:

$$l = \frac{r_b}{\sigma_b^2}$$

Using this result and the application of diversification to reduce
volatility, we can look at the ideal leverage ratio as a function of
assets in our portfolio:

![Leverage vs Number of Assets](/assets/l.png)

We can see that the optimal leverage for maximizing the geometric growth
of our portfolio increases quickly relative to the number of assets in
our portfolio but also rapidly stabilizes at a leverage between 4.5 and
5 between 2017-01-01 and 2019-01-01.

Conclusion
----------

In this post we arrived at several important conclusions. We can easily
reduce our volatility through diversification, even when picking random
assets for our portfolio. Not only does this reduce our risk, but it has
the potential to boost our returns as well. Taking it a step further, we
can actually lever up to maintain risk parity if we so choose. Thus we
can use diversification in one of two ways: to either greatly reduce
risk and modestly boost the compounded returns of our portfolio, or to
lever up the less risky diversified portfolio in order to maximize the
long-term geometric growth. Either way, diversification is a powerful
tool in an investor\'s toolbox and should be exploited to the it\'s
fullest potential. Furthermore, because diversification reduces
volatility drag and boosts our returns, in addition to allowing us to
take more leverage, it very well might make sense to diversify past the
point of a ME portfolio, as the long-term compounded savings could
outweigh the decrease in single-period expected return.

Thanks for reading, I hope this was entertaining and informative! If you
want to check out the Quantopian notebook I made for this post, click
[here](https://www.quantopian.com/posts/diversification-risk-and-leverage)!
Feel free to experiment with different start and end dates, number of
assets, or trials. If you clone the notebook and play with it, you must
also put a file called \"SP500.csv\" in your data directory. Simply copy
the data off of Wikipedia or some other source and format it to be a one
column CSV file with the header \"Ticker\".

\(1) Check out my deep dive into volatility and leverage: [ETFs,
Volatility and Leverage: Towards a New Leveraged ETF Part
1](https://smabie.github.io/posts/2019/10/04/vol.html). It clarifies
some of the concepts in this post derives the equation for leverage that
we used in the previous section.
