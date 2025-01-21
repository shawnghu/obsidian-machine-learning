https://arxiv.org/pdf/2405.15071
May 2024, Ohio State and CMU

A paper in the style of the original grokking paper: toy models, 

Connections to the central concepts of "what makes a model capable of reasoning" and "generalization to out of distribution data".

- Subtlety about what they call "reasoning":
	- ` We conceptualize reasoning as the induction and application of inference rules, and expose the model to a mixture of “atomic facts” and “inferred facts” (which are deduced from the atomic facts via a set of latent rules), resembling “axioms” and “theorems” in a formal system. To evaluate how well the model learns the rules, we test its ability to make novel deductions (i.e., completing unseen inferred facts)`

- Remarks about what they call "out of distribution":
	- Their specific setup is to generate artificial "atomic facts", separate them arbitrarily into ID and OOD, then to generate "inferred facts" by combining "atomic facts". Then they train the network on some proportion of "inferred ID facts". ID generalization performance is measured by OOD performance is measured by our ability to correctly identify "inferred OOD facts".
		- To be clear about what results they claim, we always generalize to ID (the setup is designed so that this always happens in a grokking-like way) and we *can* generalize to OOD for comparison tasks and *do not* generalize to OOD for *composition* tasks.
			- I suspect the distinction between performance on the tasks is partly artificial. Maybe comparison is slightly harder but I believe it should fundamentally be doable by transformers of approximately this scale. (They do do experiments with other transformers up to 6x as large, and claim no qualitative difference in the OOD performance.)
				- Their mechanistic analysis of the learned circuits for the two tasks focuses somewhat on the incentives of the memorization strategy vs the general strategy, so failure on "composition" seems likelier to me to be an artifact of the way the particular task is structured rather than its inherent complexity. This may be viewed as very interesting or uninteresting depending on who you are. 
	- Their stated perspective:
		- `OOD generalization aims to evaluate the systematicity acquired by the model, namely, the ability to apply rules over knowledge regardless of its distribution
			- I think this is a good narrowing of focus. It is also possible to focus on problems caused by data which was simply not seen, e.g in the in-context learning setting.
			- Related key observation: Here "knowing" a fact is always having it "memorized" in the weights of the model. I don't believe this result has much direct bearing on observations/ideas about in-context learning. Then we need to be critical about their specific notion of "OOD". To me, generically learning to "reason" includes being able to zero-shot reason about new "facts".
				- However, since we are trying to measure only the model's reasoning capacity, this is quite a reasonable thing to do; in the toy model setting they are able to ensure that the "OOD atomic facts" are learned, i.e, this is just one way of seeding their ability to get inferred statements about "OOD" elements correct.
				- It's also appropriate to call these things "OOD" in the sense that there is no particular incentive in training for the learned general mechanism to generalize to these examples; we can define a partial function which only "works" on input in a certain distribution.
				- More generally, always distinguish between things learned by training, fine tuning, in-context, or retrieval. They're mechanistically different.
	

- **What is their choice of embedding for the synthetic facts?**
	- I cannot figure the answer to this question out by reading the paper, and the repo is not easy to immediately start using (I cannot figure out how to download data necessary for it to run) / does not contain illustrative examples.
	- However, for the studies on existing SoTA LLMs they are forced to "translate" to natural language, so their observations are on some level valid for natural language and also clearly their synthetic experiment isn't done in purely natural language.
- They have another specific story about under what conditions grokking happens: they first observe that the input distribution of data affects the speed of grokking (so there is a "training stories"-type perspective). Specifically, a high ratio of "inferred" (i.e, more complex) facts to "atomic" facts leads to grokking significantly faster.
	- The mechanistic explanation for this task is that grokking is the result of (following the common explanation (is this story widely accepted?)) the incentives encountered during training: the generalizing solution has lower "complexity" (here they use the word complexity to generically launder between an intuition and the model's regularization incentives), and so we will descend towards it faster
	- They also say something about 
	- Also look into references about memory-sharing mechanisms: memory augmentation and explicit recurrence

- They claim that "grokked" transformers are superior at reasoning in large part because their knowledge representation is "parametric", and that this is still effectively superior to the performance of LLMs even with retrieval augmentation for an artificial task with large search space.
	- I can't know how good the baselines they implemented are or if there are any errors. As a matter of verifying empirical fact it would help to know qualitatively about how good RAG usually is.


References:
[Universal Transformer]()