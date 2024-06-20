Try to look ML: NeurIPS ICML ICLR 
Interpretability are these 3: ACL NAACL EMNLP

#### IBG

[Mechanistic interpretations] -

[https://arxiv.org/abs/2211.00593](https://l.messenger.com/l.php?u=https%3A%2F%2Farxiv.org%2Fabs%2F2211.00593&h=AT0HK5OSshWug6_ZfooKvTWSCfcVlf5lmyHU60nrFsq5RK0PPLVpHKevlCawylVLB2R53A2BMCExu8OYeZpl7NcUwWmETKM-RN2TGLHF0iru59Jo6w_u_nZzTJTPfUn4ood3V0BlJEUccg)

- Anthropic circuit threads [Causal interpretation for ML] -

[https://doi.org/10.48550/arXiv.2003.03934](https://doi.org/10.48550/arXiv.2003.03934)

-

[https://doi.org/10.1080/07350015.2019.1624293](https://l.messenger.com/l.php?u=https%3A%2F%2Fdoi.org%2F10.1080%2F07350015.2019.1624293&h=AT0HK5OSshWug6_ZfooKvTWSCfcVlf5lmyHU60nrFsq5RK0PPLVpHKevlCawylVLB2R53A2BMCExu8OYeZpl7NcUwWmETKM-RN2TGLHF0iru59Jo6w_u_nZzTJTPfUn4ood3V0BlJEUccg)

[Model editing] -

[Locating and Editing Factual Associations in GPT](https://doi.org/10.48550/arXiv.2202.05262)
- Prose is not very clear, either in wording or in terms of the intention or relation of various ideas. The experiments are pretty thorough, however.
- [[But is it really in Rome? An investigation of the ROME model editing technique||There is a fairly strong criticism of this paper]]
- While the result is cool for what it is, it seems extremely far from a sure bet and I'm pretty sure people wouldn't want to use this technique as-is. Mostly, we're not that sure about what actually happens to the representation of the knowledge within the model. Ultimately, there's a fundamental question about what the desired behavior is if you modify certain facts, especially since most facts are enmeshed in webs of "general knowledge".
	- e.g, if you simply tell it that "the Eiffel Tower is in Rome", there are several questions it now has to BS in order to answer, e.g, "tell me about the construction of the Eiffel Tower", or "How can I get from the Eiffel Tower to the Musee d'Orsay?" or even something just incidentally tied in, like "When was the Eiffel Tower built?" It's just not clear what the desired behavior is or why you would want to do this. Modifying specific "facts" is actually something you very rarely want to do. Human updating of understanding of things is a little bit more subtle than that in most cases.

-

[https://doi.org/10.48550/arXiv.2004.12265](https://doi.org/10.48550/arXiv.2004.12265)

-

[https://doi.org/10.48550/arXiv.2101.00288](https://doi.org/10.48550/arXiv.2101.00288)


## Authors

### Kevin Wang
Can't find anything about this guy, maybe because there's 1000 people named this.

## Buck Shlegeris
I knew this guy previously. He works on a specific kind of theory, involving deceptive agents and schemes for controlling powerful AI; not a lot related to model editing or interpretability.

## Alexandre Variengien

[# How does GPT-2 compute greater-than?: Interpreting mathematical abilities in a pre-trained language model](https://arxiv.org/abs/2305.00586)
- This is fundamentally extremely similar to the original path patching paper, it just does it for a different task (or rather, collection of related tasks).
	- This makes sense; it Variengien was on the original path patching paper and also at Redwood Research and also this paper cites that paper.
	- Concretely:
		- `GPT-2 small’s final multi-layer perceptrons boost the probability of end years greater than the start year`
- I don't think it's a good idea to do many studies of this type on GPT-2 specifically, especially since we've seen in other places (e.g, the logit lens notebook) that GPT-2 and other models vary significantly in their internal behavior.
- It's otherwise quite thorough and clearly explained.
	- They do a large amount of neuron/activation level studies, e.g in section 4.2 they use logit-lens analysis and some logical deduction to make statements about how the greater-than operation can be computed.
		- But again, I don't think focus on the exact mechanisms used is valuable, as much as the knowledge that a mechanism can exist to perform a specific task

- Quotes:
	- `three increasingly different prompts: “The <noun> started in the year 17YY and ended in the year 17”, “The price of that <luxury good> ranges from $ 17YY to $ 17”, and “1599, 1607, 1633, 1679, 17YY, 17”. In all cases, a two-digit number greater than YY would be a reasonable next token`.
		- `Similar tasks seem to use similar, but not identical, circuits.`, based just on observing this fact directly on the last task
	- `The lack of causal evidence for the role of structured number representations, and the fact that GPT-2 cannot handle related operations like “less-than” or “equal-to” argue against generalized math mechanisms`
- Weakening arguments:
	- Unfortunately the analysis seems to fall apart at the largest level, severely weakening the impact of the rest of the analysis: this exact paper states that `The chosen task should:[...] Be solvable by your model: if your model cannot solve the task, there may be no circuit. At minimum, the model should exhibit consistent behavior`, but they do spend a significant amount of time studying and explaining tasks that this model fails at through the lens of the circuit they identified.
		- `GPT-2 even failed at some tasks that were solvable using the greater-than circuit, like “17YY is smaller than 17”`
		- `We also observe the opposite phenomenon: inappropriate activation of the greater-than circuit, triggered by prompts like “The <noun> ended in the year 17YY and started in the year 17” and “The <noun> lasted from the year 7YY BC to the year 7”`... `GPT-2 thus overgeneralizes the use of our circuit.`
		- Given the above two quotes, it's hard to say concretely that the circuit "successfully performs the task" when there are examples where it should be used where it isn't used, and there are examples where it shouldn't be used where it is used. 
			- Put differently, maybe we have a circuit that performs "greater than", but the model doesn't actually know how to use it, so bottom line, what statements can we make about the model behavior?

[# Look Before You Leap: A Universal Emergent Decomposition of Retrieval Tasks in Language Models](https://arxiv.org/abs/2312.10091)

## Jacob Steinhardt

This guy has a lot of papers, several of which are intriguing, but not too many of which are directly related to mech interp or model editing.
- [Overthinking the Truth: Understanding how Language Models Process False Demonstrations ](https://arxiv.org/abs/2307.09476) uses mechanistic ideas to try and interpret the core phenomenon of the paper.
- [Interpreting the Second-Order Effects of Neurons in CLIP](https://arxiv.org/abs/2406.04341) isn't that closely related either, but it seems to involve the good idea of "automatically describing [neurons]", which helps with the scale critique I have of other papers.
	- [[CLIP]], using a vision transformer to classify images with various text outputs as the label classes.
	- Their approach sort of "supersedes" the logit lens approach, by also taking note of second order effects (and to a lesser extent, "indirect effects").
	- The results they show to prove the validity of the second order effects are basically activation patching, as I understand it, and the result is pretty powerful because hte fact that it was done in an "automated" way shows that it works "at scale", at least for CLIP (a lot of this would carry over to other transformers, though).

## Kevin Meng
[Mass-Editing Memory in a Transformer](https://arxiv.org/pdf/2210.07229)
- This guy did the other transformer editing paper, so this isn't that surprising to see.
- Supposedly a lot of other direct model editing techniques or "knowledge update" techniques don't scale to many examples well.
- This paper has many of the same conceptual limitations of the other "modifying facts" papers, as well as currently being limited to the scope of "subject object relation" knowledge schemas.
	- It actually also points out another one really clearly: They edit Michael Jordan to be a baseball player-- does this mean he was never a basketball player (ie, there was a mistake in the knowledge base before) or that he just switched sports (ie, the external world has changed)? Isn't it extremely important to distinguish between these, especially if we ask something like "what did michael jordan do in 1985?"
	- Most damning is this: `for example, the association that “Tim Cook is CEO of Apple” must be processed separately from the opposite association that “The CEO of Apple is Tim Cook.”`
		- If you claim to be editing the model's understanding of facts, isn't this like the lowest possible standard for achieving that?
	- Now standard provisions about research apply: we never know what'll be useful before it really comes through, but let's say this doesn't suit my tastes.
- The core contribution of the paper is a functionally similar method to the old paper, but with a mathematical update which uses matrix calculus (and some assumptions of linearity) to compute an update rule for a layer with respect to many different MLP layers at once. Mathematically, they also make some consideration for the fact that updating the earlier layers will have an effect on activations in later layers, and propose a method for manually "spreading out" the update magnitude across the MLP layers they deem eligible (by the same analysis for which layers are important as the previous paper).
- Their results are far superior to ROME on the metrics that they've defined for scales of several thousand edits, but they compare sometimes competitively with another method called FT-W, which by context is a much simpler method.
## Trevor Hastie
Lots of papers in nearly pure statistics. Happens to have been a coauthor on [[Surprises in High-Dimensional Ridgeless Least Squares Interpolation]]. Not much on arxiv having to do with model editing. Recently published a paper with Stephen Boyd!

## Qingyuan Zhao
Also mostly statistics and applied statistics, not always to computer science per se but often to data science.
## Other papers

- [Modifying Memories in Transformer Models](https://arxiv.org/pdf/2012.00363), cited by the model editing paper.
	- It's a straightforward paper with clear prose.
	- Basically entirely empirical in nature.
	- Core idea: just do a fine-tuning on new facts in order to update them, but in order to avoid forgetting old facts, enforce a constraint on the maximum deviation of the parameters directly.
		- The choice of what the maximum deviation should be
		- They choose the L-inf norm for empirical reasons.
			- Since they do this, it's somewhat straightforward to enforce the constraint by just clipping gradients.
	- One of its contributions is to do the work to generate a new dataset, against which we can measure the performance of "modified fact integration", which basically just tests how thoroughly we believe the modified fact and how badly we perform on "unrelated facts". 
		- As mentioned elsewhere, though, when is a fact unrelated?
		- Moreover, they are sort of only able to demonstrate this on fairly simple compositions of facts, because they had to generate the dataset programmatically.
	- They find generally that things work best when they use their method, as opposed to doing something like just training on a mixture of old and new data. They also find that it works better across a couple of models to constrain the fine-tuning to a subset of the model (typically, a single transformer block). Again, they find these things empirically, which I find pretty uncompelling, since I don't know their strategy for picking blocks or how many things they sampled.
	- Other statistically expected things happen, like if you increase the number of "modified facts", then eventually you need more parameters to be fine-tunable or else there won't be enough model capacity to accommodate them.
	- It's interesting that they find empirically that models will catastrophically forget much of their knowledge when trained on a relatively small set of modified facts. Are we sure this isn't just an artifact of the way they're doing the fine-tuning (e.g, learning rate too high)? After all, don't most LLMs have to learn a bunch of new facts without forgetting old ones too badly?

