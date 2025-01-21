[Scaling Monosemanticity: Extracting Interpretable Features from Claude 3 Sonnet](https://transformer-circuits.pub/2024/scaling-monosemanticity/index.html)
- How did they test model activations on images?
- How are they visualizing feature activation? Simply put the prompt through and look at the number, or dot product with feature?
	- What does it mean to clamp features? Just add in the direction of the feature (thereby affecting other features by a small amount)?
- What is a [scratchpad](https://arxiv.org/pdf/2112.00114)?
- How are they automatically annotating features?
- Is the L1 loss really the best way to get an AE to be sparse? See [Anthropic's experiment](https://transformer-circuits.pub/2024/feb-update/index.html#dict-learning-tanh)

### Remarks on research agenda
[Core views on AI safety](https://www.anthropic.com/news/core-views-on-ai-safety)

- Nice observation: certain phenomena suggested by theory didn't happen (problems with local minima); other interesting phenomena failed to be predicted by theory (adversarial examples); I think this is generally how knowledge acquisition progressed in human history
- Anthropic is betting hugely on mechanistic interpretability as a way of dealing with deception.