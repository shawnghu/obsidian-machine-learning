---
tags:
  - Papers
---
https://mathai-iclr.github.io/papers/papers/MATHAI_29_paper.pdf
https://www.youtube.com/watch?v=dND-7llwrpw&feature=youtu.be
ICLR 2021, OpenAI

- fairly clear paper with simple premise and clear language
	- (with only one small exception, which is the term "optimization budget")
- I very much like the algorithmic dataset approach, it allows for a lot of control with which to develop theory:
	- `Such experiments can be quickly reproduced on a single GPU, and this makes them convenient testbeds for theories of generalization.`
		- Yes, one of the difficulties of deep learning seems to be the very long iteration time, but these could theoretically provide feedback in minutes or even seconds.
			- And the algorithmic nature of the datasets allowed them to do 30+ morally similar runs to see if the effect is robust, which is far nicer than what interpretability people have to do with the singular GPT2 (or more generously, the 10-ish GPT2 class models that are open-sourced)
- The overwhelmingly shocking thing in this paper is that validation error can change so much long after the model has overfit to the training set.
	- At the very least, this implies that the parameters are still changing, otherwise the model behavior couldn't change at all, much less have the validation performance improve so drastically.
		- This [[On the idea that "intuitions can be violated in higher dimensional spaces"||violates the often intuitive idea]] in three dimensions that when we fit to the training data, we are settled at the bottom of a basin; it seems instead that the set of points that perfectly fit the training data are probably a high-dimensional manifold with lots of room to maneuver around.
			- This suggests a question, that I don't know how to answer: [[How difficult is it to reach a local maximum in a very-high dimensional space?]] On a related note, how many parameters does the toy transformer that they use have?
		- It would be extremely nice to have a graph of the training loss overlaid on the graph containing the training performance and the validation performance.
			- Actually, in fact that's what Figure 4 in the paper is. It shows that the training loss remains more or less stable extremely close to 0 (keep in mind, 100% correct predictions doesn't necessarily mean 0 loss, so this is new information, but now what I want is to see the zoomed in or scaled training loss to see if it shows any substantial trends), while the validation loss oscillates wildly and increases to a very high level before descending slowly from like iteration 8000-10000
	- They reproduced this result, though less sharply, with full batch gradient descent, so it exists independently of the "stochasticity regularizer" thing people are talking about.
		- (Although the SGD thing makes the validation happen faster, but I wonder if that's just an artifact of the way they measure iterations (hopefully))
	- Also re: their variable optimization algorithms experiments, intuitively, why should weight decay make the generalization happen faster in this setting?
		- It would be very nice to get to see the graph of just the L2 loss over time. Does grokking happen when the L2 loss goes below a certain point?
			- A just-so story goes like this. First we rapidly descend to some point by overfitting to the training set. But then the L2 penalty helps to "break down" the representation of the memorized and actually guide the parameter vector to a more "optimal", or more "sparse" representation?
				- Intuitively to me, it is necessary for the model to be [[On the benefits of overparameterization in neural networks||overparameterized]] in order for there to be room for this to happen, otherwise going away from the memorized dataset is always actually reducing our training performance, so gradient descent won't allow it.
	- I believe a paper like this is an extremely good candidate for mechanistic interpretability-like approaches. What can we discern about (the algorithms implemented after overfitting to the training dataset) versus (the algorithms which actually generalize to the test dataset) versus (the algorithm encoded by the NN right before it starts to improve in test error)? and with a network this small and dataset this interpretable, can we make any connections between the optimization dynamics of the parameters and the nature of this algorithm?
		- Damn, Neel Nanda figured this out within a year of this paper coming out: [[Progress Measures for Grokking via Mechanistic Interpretability||paper]]
		- Also my ideas about using this to gain some insight on optimization dynamics may be covered by [[Hidden Progress in Deep Learning- SGD Learns Parities Near the Computational Limit||this paper]].