---
tags:
  - Papers
---
https://openai.com/index/deep-double-descent/, https://windowsontheory.org/2019/12/05/deep-double-descent/
https://arxiv.org/pdf/1912.02292
December 2019, Harvard and OpenAI, previously observed in https://arxiv.org/abs/1812.11118, December 2018

- In general, we need to distinguish between epoch-wise, data-wise, and model-wise double descent, because the phenomenon occurs with all of them.
	- They introduce the notion of Effective Model Complexity (EMC) of a *training procedure* (with respect to a distribution), which is roughly the number of samples from D that T can produce a model to fit.
		- Note that a training procedure implicitly involves selecting from a family of models, training for a shorter or longer period of time, 
- Post notes that double descent phenomenon is stronger in the model-wise case when there is label noise, but also point out that the data-wise example occurs with no label noise.
	- They do some discussion later about the nature of label noise; 
- `_In general, the peak of test error appears systematically when models are just barely able to fit the train set._ Our intuition is that, for models at the interpolation threshold, there is effectively only one model that fits the train data, and forcing it to fit even slightly noisy or misspecified labels will destroy its global structure. That is, there are no “good models” which both interpolate the train set and perform well on the test set. However, in the over-parameterized regime, there are many models that fit the train set and there exist such good models. Moreover, the implicit bias of stochastic gradient descent (SGD) leads it to such good models, for reasons we don’t yet understand.`
	- To re-emphasize, there must be some biases to the training process (+ the datasets we tend to use?) that allow for generalization where classical statistics would not predict.
- The second post uses the classic polynomial fitting example to illustrate the point: a degree 1000 fitting does "better" on ~15 points than a degree 20 one does.
	- But a commenter astutely points out that while the result looks intuitively better, how the result is optimized for depends on a choice of basis:
		- `In particular, the fitted curve is sensitive to how the basis vectors are normalized. While Legendre polynomials are orthogonal, they are not orthonormal: the n-th polynomial has l2 norm sqrt(2/(2*n+1)) (see [https://en.wikipedia.org/wiki/Legendre_polynomials](https://en.wikipedia.org/wiki/Legendre_polynomials)). This means that the gradient-descent (or minimum-l2-norm) solution using the standard Legendre polynomial basis has a natural preference for lower degree basis vectors (which have a larger norm), and this inherent “regularization” looks to be very important for avoiding overfitting in the high-dimensional case.`
		- Supposedly choosing basis does in fact make the 1000-degree case look worse, maybe in terms of integral of squared error.
			- Reply: This begs the question— “do operations such as rescaling of features break double descent? ” We don’t know for sure, but analysis of the linear regression problem suggests that it does not. Advani & Saxe 2017 [[Surprises in High-Dimensional Ridgeless Least Squares Interpolation]], Mei & Montenari 2019 [[The generalization error of random features regression Precise asymptotics and double descent curve]]
			- But furthermore, even the worse version of the 1000-degree case isn't bad in the same way the 20-degree one is.
		- I believe that more [toy model experiments]() will be good for study of theoretical phenomena like this.
	- Adding regularization can cause the phenomenon to disappear.


## Related Papers:
- [Grokking: Generalization Beyond Overfitting on Small Algorithmic Datasets](https://mathai-iclr.github.io/papers/papers/MATHAI_29_paper.pdf)
	- ICLR 2021, OpenAI
	- 
