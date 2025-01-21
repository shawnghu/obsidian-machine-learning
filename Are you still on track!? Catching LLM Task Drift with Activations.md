https://arxiv.org/pdf/2406.00799

These guys directly study the question of whether we can predict or observe 
They find that a linear probe trained on the concatenated activations at the last sequence position is really good, with an ROC AUC of over 0.99. Actually, most individual layers' information is enough to train a classifier with ROC AUC > 0.99.

Their original setup includes a prompt, but they experimentally find that it is not actually necessary and you can just look at activations in a normal context, which I think they should've emphasized.

They also mess with some metric learning stuff, which is a bit weaker but also works.

They seem to suggest that their method is robust to attacks other than the specific type that they train on for discrimination. They show this just by coming up with a few normal prompt injection looking attacks and showing that their classifier correctly identifies them.


## Meta-analysis / Outside view thoughts
- Their value proposition is pretty large: if their technique works as well as they say it does, it should be possible to severely hinder most prompt injection attacks at extremely low cost, and their idea is really simple, so I feel someone would've thought of this already.
- Loosely using analogies to human System 1, it's perfectly plausible that the model has features corresponding to "a sudden context or task shift seems to have occurred". Then a linear probe should be able to make use of them easily.
- The function vectors paper attempts an extremely similar approach, except that they are trying to transfer behavior instead of classify it. But the function paper results are quite weak, so there seems to be a slight contradiction here.
	- It's totally possible that these activations contain enough weird information that directly patching is a bad move, but they also contain the necessary information to do classification well.
