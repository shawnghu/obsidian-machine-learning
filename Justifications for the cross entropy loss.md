*Or for maximizing the log-likelihood instead of anything else*

- Log likelihoods tend to be more computationally tractable, since they:
	- sum over log(loss for example)
	- involve logarithms, which are more numerically stable
- also there's the thing that actually gives the CE loss its name: `cross-entropy between two probability distributions p  and q , over the same underlying set of events, measures the average number of bits needed to identify an event drawn from the set when the coding scheme used for the set is optimized for an estimated probability distribution q , rather than the true distribution p`
	- Or cross-entropy := $H(p, q) = -E_p(log(q))$.
	- This is also H(p) + KL_divergence(p || q), so given that the entropy of p (the label) is fixed, minimizing the cross-entropy between p and q minimizes the KL divergence between the two.
		- In this case, we're thinking of the label as a distribution over the possible label values, but I think we can generalize this to make SGD implicitly minimizing the divergence of two more general distributions.
- Now to be clear, the actual loss function is the cross-entropy between the two vectors: $sum_{i} (p_i * log(q_i))$, where the i are the entries in the vector/the possible labels/the support of the distribution
	- But also in the supervised learning setting with labels of a single class most of these terms go to zero, since $p_i$ is zero for all but one entry.

https://stackoverflow.com/questions/17187507/why-use-softmax-as-opposed-to-standard-normalization has a great second answer (the first answer, less so).
- `The exp in the softmax function roughly cancels out the log in the cross-entropy loss causing the loss to be roughly linear in z_i. This leads to a roughly constant gradient, when the model is wrong, allowing it to correct itself quickly. Thus, a wrong saturated softmax does not cause a vanishing gradient.` (Note that this depends on the assumption we're doing log likelihood maximization/using the cross-entropy loss already.)

https://stats.stackexchange.com/questions/145272/how-is-softmax-unit-derived-and-what-is-the-implication/145277#145277 justifies things using the terms "maximum entropy distribution" and "exponential family".
- `In summary, the multinomial logistic function falls out of three assumptions: a support, a sufficient statistic, and a model whose belief is a combination of independent pieces of information.`
 https://stats.stackexchange.com/questions/162988/why-sigmoid-function-instead-of-anything-else/318209#318209

 https://willwolf.io/2017/04/19/deriving-the-softmax-from-first-principles/