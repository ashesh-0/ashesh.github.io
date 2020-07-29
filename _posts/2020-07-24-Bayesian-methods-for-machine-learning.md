---
---
This post will be a summary of my understanding from the coursera course [Bayesian methods for Machine learning](https://www.coursera.org/learn/bayesian-methods-in-machine-learning).

Let me first honestly admit that this page was not created by me to either educate the uneducated or to make myself believe that the educated ones will recognize me as an educated fellow after glancing through this post (Btw, if you are a professor and I've requested you for PhD position, know that I'm super educated :P). It was not even created to make my website have more content. It was mainly created because I was finding it difficult to understand quite a few papers by top notch people. And the reason was that they had something to do with VAE or gaussian processes. So I thought it to be high time to revise.

Let us begin with terminology. Here, we will have $$\theta$$ as model parameters, $$X$$ as the data. $$X$$ includes the target variable as well.

* $$P(X\|\theta)$$: Likelihood: Probablity of data given the parameters.
* $$P( \theta\|X) $$: Posterior- Probablity of the parameters given the data.
* $$P(\theta)$$: Prior: Probablity distribution of parameters.
* $$P(X)$$: Evidence: Probablity distribution of data.


In the real world scenario where we want a model to predict something, we already have some training data. So data is given and one wants to get to a good parameter set for their model. So **Posterior** is then what you want. Knowing it, you can then sample your parameters and work with them. Or you can choose to be a stubborn purist Bayesian and get your prediction by integrating over the Posterior.

>When number of data points is must larger than number of parameters then maximizing Likelihood can work. However, bayesian approach, which is to optimize the Posterior can work with small data as well.

Unfortunately, they did not explain why that is the case, but to me, this was pretty significant.

## Bayesian Network
It is simply a way to define a bayesian model. It has nodes which are random variables and it has edges which encode direct impact between the variables. We can write the joint distribution over variables $$X_1,X_2..,X_N$$ as
\$$P(X_1,X_2,.., X_N) = \prod_{i} P(X_i|Pa(X_i))$$

Naive Bayes classifer makes the naive (yet pretty effective) assumption that all the feature random variables $$F_i$$ are independent conditional on the target variable $$Y$$. So, the joint probablity distribution looks like
\$$P(Y,F_1,F_2..,F_N) = P(Y)* \prod_{i} P(F_i|Y)$$

## ML Estimate (a way to estimate $$\theta$$):
ML stands for Maximum likelihood. We pick the theta having maximum Likelihood, or $$P(X|\theta)$$.
## MAP Estimate (another way to estimate $$\theta$$):
MAP stands for Maximum a posteriori probablity. A posteriori probablity means Posterior, or  $$P(\theta|X)$$. In MAP, we pick the theta having the maximum posterior. It is also called as *point estimate* since we are satisfied with one point in theta distribution instead of working with the whole distribution.

## Issues with MAP Estimate
It can happen that there is not enough probablity density in nearby region of the MAP estimate. In that case, the model's performance will be super sensitive to perturbations to the estimate, or $$\theta_{MAP}$$. And then there is no quantification of the sensitivity. We don't know how much the performance will degrade if we change the $$\theta$$ by some amount.

In a practical sense, a way to partial solve these problems is to be able to sample multiple $$\theta$$s from the posterior. Average the prediction obtained from each $$\theta$$ to get a final prediction. This prediction will be less sensitive to perturbations in $$\theta$$ and we can easily compute the standard deviation from individual predictions.

## Conjugate Distributions:
When we try to model a problem, we typically fix the likelihood and prior. Using bayes rule, we know that $$P(\theta|X)=\alpha * P(X|\theta) * P(\theta)$$. Note that in Bayesian methods, we try to maximize the posterior ($$P(\theta|X)$$). The maximization task would become really easy if the posterior is a known distribution. That's where the conjugate distribution comes in.

>Prior is said to be conjugate of Likelihood if Prior is in same distribution as Posterior.
One easy example is that if both prior and likelihood is normal distribution, then posterior also becomes normally distributed.


## Issues with Regression models:
Before the course delves into bayesian model, it is prudent to first know disadvantages of using regression models. One major issue with them is that they lack a principled approach to handle missing features. Other issue is that they cannot quantify uncertainty in prediction. For example, for a binary classification task, if the predicted probablity is 0.5, then there are two explanations for it. One is that model has not seen this kind of input and has no clue about which class should it belong to. The other possibility is that model has seen this kind of data and knows that it is equally likely to belong to either class.

## Latent Variable Models
Idea is to introduce some hidden variables whose value is not known for training as well as validation set. However these variables have semantic importances in some cases which we will see for gausian mixture models.
### Gaussian mixture models:
This is a model to solve the clustering problem. Number of clusters is not known. Given a set of data points, one needs to cluster them in groups. Here, we will create a latent variable T to denote the cluster number. So it can vary in range $$[1,2,..K]$$ where K is the maximum cluster count. GMM adds the contraint that points for each cluster comes from their respective gaussian distribution. Mathematically speaking,
\$$P(x|T=c) = N(\mu_c, \sigma_c)$$

In latent variable models in general , the metric to optimize is very intuitive: maximize the probablity of data. We would like to maximize $$P(X)$$. Few lines of maths written below outlines the approach taken to solve the problem.
$$log(P(X)) = \sum_{i} log(P(x_i)) = \sum_i log(\sum_j P(x_i,t=j))$$
$$ = \sum_i log(\sum_j P(x_i|t=j)*P(t=j))$$
$$ >= \sum_i \sum_j log(P(x_i|t=j))*P(t=j)$$

The inequality in last line used the fact that log is concave function and for any concave function f, $$f(\sum_i w_i*x_i) >= \sum_i w_i*f(x_i)$$, where $$w_i$$ sum to 1 and are non negative.
