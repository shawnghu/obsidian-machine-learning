---
tags:
  - Papers
---
Way back in 2015; I remember reading about this and giving up in grad school
https://arxiv.org/abs/1503.02406
https://www.youtube.com/watch?v=XL07WEc2TRI&t=1102s
There is some controversy; purportedly debunked by *On the Information Bottleneck Theory of Deep Learning* https://openreview.net/pdf?id=ry_WPG-A- 
- There is then some dispute about whether this debunking was actually scientifically sound. It seems there's no major consensus even today.
- I am missing a lot of what I need to know about information and complexity to even follow a lot of discussion.

Related:
[[Invertible Neural Networks]]

Discussion:
- https://www.reddit.com/r/MachineLearning/comments/n06bp2/d_understanding_the_bottleneck_principle_in/
	- `First, the Information Bottleneck Principle _is not_ the same as bottleneck layers in networks like auto-encoders. These can serve as information bottlenecks, but the principle is far more general.`
- https://www.reddit.com/r/MachineLearning/comments/em3ynp/d_trying_to_wrap_my_head_around_the_information/- 
	- `The thing is that optimization alone cannot explain the enormous generalization abilities of DNNs.
	- `Optimization justifies that we reach a high accuracy on the training set after training, but why does the DNN perform so well on the validation/test set?`
	- `If you train CNN and a large Fully-cennected network (MLP) on image data, both model will achieve 100% training accuracy eventually. However, the CNN gets a much higher test performance. Why?`
	- `If you train a CNN with standard SGD and another one with Adam, then the one trained with Adam will converge much faster, but achieves a slightly worse test accuracy. Why? (The "flat minima" fairytale has been debunked)`
	- `A 1-hidden layer MLP can approximate any function arbitrarily close (Hornik et al. 1989). So why does a deeper network generalize better than a 1-hideen layer MLP with a large number of units?`
- https://www.reddit.com/r/MachineLearning/comments/be8qie/discussion_what_is_the_status_of_the_information/
	- `doesn't the observation that RevNets and reversible Normalizing Flows work pretty much kill the Information Bottleneck Theory`
	- `Neural networks transform inputs to outputs. The networks have the ability to memorise data exactly. They do this first as it’s an easy route to predicting the output effectively. After this happens the dynamics change. In order to be robust to all of the noise in the training process the networks start to compress the information they are receiving. Losing all possible irrelevant information about the input, while preserving all necessary information about the output.`
	- `There might be a subtelty here. NNs are generally working on continuous variables, not discrete ones. The statement that applying an invertible transformation retain all information is only true for discrete random variables.`
		- `It is true that a smooth invertible transformation of a continuous variable can change the differential entropy, but my understanding is that such a transformation does not affect mutual information because the determinants cancel.`