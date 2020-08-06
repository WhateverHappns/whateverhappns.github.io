# Hidden Markov Models
- "The HMM works for dependent observation data *sequences*"
- What is a conditional probability distribution?
    - Different from the marginal probability distribution, the CPD is the probability distribution of _X_ given _Y_, 
    whereas the marginal probability distribution is the distribution of _X_ without reference to _Y_.ith a modification in calculating probabilities of observations."
- The basic elements of an HMM for multiple observations are:
![Hidden Markov Model Observations](https://github.com/whateverHappns/QuantProject/blob/master/images/HMM-Observations.png)
- [Markov Chains](https://en.wikipedia.org/wiki/Markov_chain#Economics_and_finance)

## Own ideas
- Consider using the high and low as opposed to the close price returns## Own ideas
- Pick up on when the most likely (ahh, again) probabilities were wrong because that's by definition an anomaly.

## Understanding the model 
- Apparently, the model assumes statistical independence of each observation,
which makes sense for the M&M or urn examples, however for stocks, it doesn't.
There very much exists a statistical dependence on the previous observation 
because the traders react exactly based on that. (at least the technical ones)

## [Viterbi algorithm](https://en.wikipedia.org/wiki/Viterbi_algorithm)
- Used to find the **most likely** sequence of hidden states. 
- Check "Learning the algorithms.ipynb" for the algorithm in python
- hmmlearn uses it in cython, if I will write these algorithms myself, it might be fruitful to consider doing so in cython because it's apparently way faster.
- As mentioned above, it finds the maximum likelihood for the next probability which is apparently not the best choice since it's a *frequentist* approach. 

## [Forward-Backward algorithm](https//en.wikipedia.org/wiki/Forward%E2%80%93backward_algorithm)
- Is it for both multiple and single observation HMMs?

## Robert, C. P., Ryden, T., & Titterington, D. M. (2000). Bayesian inference in hidden Markov models through the reversible jump Markov chain Monte Carlo method. Journal of the Royal Statistical Society: Series B (Statistical Methodology)
- Hidden Markov models form an extension of mixture models which provides a flexible class of models exhibiting dependence and a possibly large degree of variability. We show how reversible jump Markov chain Monte Carlo techniques can be used to estimate the parameters as well as the number of components of a hidden Markov model in a Bayesian framework.


- Way too complicated for me ATM but the conclusion sums it up pretty good:
  

   - "We have seen that it is possible to construct reversible jump MCMC algorithms for Bayesian analysis of HMMs 
with an **unknown number of componentes** (NOTE: different from the one that I've done, with 4 states. Look into that!) 
We believe such algorithms may be strong competitors to a frequentist approach based on maximum likelihood. 
Obviously, it is desirable to find dimension changing moves that achieve larger acceptance rates than those presented here. 
(NOTE: So there's room for improvement..) We make two tentative conclusions: adding strucure (Markov dependence) to a model
pushes the posterior distribution (NOTE: after what?) of *k*(?) towards smaller values. Secondly, adding structure to a model 
makes it more difficult to design split(?) or combine moves, or more generally dimension changing moves, that yield high acceptance 
rates. (NOTE: WHAT?) 


- "Since MCMC imposes significant computational burden, in cases where computational scalability is also of interest, one may alternatively resort to variational approximations to Bayesian inference." (If the Monte Carlo simulations are too crazy and I am trading on a very small time scale)
![HMM-Bayesian](https://github.com/WhateverHappns/QuantProject/blob/master/images/HMM-Bayesian.png)

## Hassan et al HMM and FL:
![HMM-FL Image](https://github.com/WhateverHappns/QuantProject/blob/master/images/HMM-FL.png)
    - "An HMM is trained using the training dataset and then the HMM-log-likelihood values calculated in the training stage (Fig. 1(a)) are ordered using a number of ‘buckets’ or ‘bins’. Each of the ‘buckets’ contains similar patterns (Fig. 1(b)) that produce log-likelihood values within the range of the bucket’s start point and end point. A recursive divide and conquer algorithm (Fig. 1(c)) is then used to generate a set of fuzzy rules. Finally, further optimization of the fuzzy rule parameters is done using a gradient descent method (Fig. 1(d))."
## Nguyet Nguyen Analysis and Implementation of HMM for Stock Prediction:
- Important part for HMMs is the indicator used as well as the models used to find ideal *number of states*.
    - This paper uses the Aikaike information criterion (AIC) and Bayesian information criterion (BIC) to get number of states. 
- "This prediction approach is based on the work of Hassan and Nath (2005). However, our procedure is
different from their method in that we apply HMM for the returns of open, low, high, and close prices,
which are independent, while the authors used the HMM directly to open, low, high, and close prices,
which are not independent" 
- ![Observation](https://github.com/WhateverHappns/QuantProject/blob/master/images/Observation-Sequence.png)
    - Does this mean **T** = **L**?
    - _L_ is number of independent observation **sequences** not variables.
- What is a conditional probability distribution?
    - Different from the marginal probability distribution, the CPD is the probability distribution of _X_ given _Y_, 
    whereas the marginal probability distribution is the distribution of _X_ without reference to _Y_.
- This paper uses HMMs with multiple observations. This is something to be figured out. What does multiple observations refer to?
I think they made one HMM for multiple stocks i.e. FB, AAPL, GOOGL. And used the information criteria tests to first see whether 
they were independent enough to be treated as "independent observation sequences". <-- This sounds a whole lot like what they do at RenTec
- Where this paper differs from the previous ones is that it puts all the stocks (independent observation sequences) into one 
Observation sequence and trains the model on that. *I think?*
    - Actually, in the abstract they say that they use **both** multiple and single observation data.
