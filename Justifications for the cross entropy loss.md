*Or, equivalently, for maximizing the log-likelihood instead of anything else*

- Log likelihoods tend to be more computationally tractable, since they:
	- sum over log(loss for example)
	- involve logarithms, which are more numerically stable
- also there's the thing that actually gives the CE loss its name: `cross-entropy between two probability distributions p  and q , over the same underlying set of events, measures the average number of bits needed to identify an event drawn from the set when the coding scheme used for the set is optimized for an estimated probability distribution q , rather than the true distribution p`
	- Or cross-entropy := $H(p, q) = -E_p(log(q))$.
	- This is also H(p) + KL_divergence(p || q), so given that the entropy of p (the label) is fixed, minimizing the cross-entropy between p and q minimizes the KL divergence between the two.
		- In this case, we're thinking of the label as a distribution over the possible label values, but I think we can generalize this to make SGD implicitly minimizing the divergence of two more general distributions.
- Now to be clear, the actual loss function is the cross-entropy between the two vectors: $sum_{i} (p_i * log(q_i))$, where the i are the entries in the vector/the possible labels/the support of the distribution
	- But also in the supervised learning setting with labels of a single class most of these terms go to zero, since $p_i$ is zero for all but one entry.