[Technical Report](https://arxiv.org/pdf/2303.08774)

- Power law scaling: It's obvious in hindsight, but this is the first time I've been lead to think about the engineering implications of scaling laws, not just the abstract alignment implications. Before sinking tons of resources into training the model, they were able to make certain predictions about the model's eventual performance with power law predictions, and verify them experimentally, e.g by testing performance on some smaller datasets/benchmarks 
	- (confounded slightly by [inverse scaling|Inverse Scaling]())

- risk surface was largely characterized by explicit human expert red teaming
- manual measurement of human preferences is still all we can really do to determine whether something follows human preferences
- `These undesired behaviors can arise when instructions to labelers were underspecified during reward model data collection portion of the RLHF pipeline.` here's another reason that RLHF output can be brittle
also of note:

how does the vision input work?
openai evals
