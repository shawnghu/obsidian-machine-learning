I haven't easily found a lot of resources on how this is done in practice. It seems to me like this is an important thing to develop a science on, and that in principle the smart engineers at various large tech companies should agree, and also money/performance/resources are clearly at stake with respect to these questions, so people will probably have actually figured out the question.

### On the importance of the attention mechanism
Possibly anything that mixes the embeddings across tokens might work.

- [Luke Melas' project](https://github.com/lukemelas/do-you-even-need-attention?tab=readme-ov-file) and [MLP-Mixer](https://arxiv.org/abs/2105.01601)by Google Research just replace the attention layer with an FC net, and the whole thing is almost as good at roughly equivalent cost.
- However, to the extent that we have open-source models, all the top ones seem to use some variant of what we would properly call "attention". 
- More on FC nets at [Gwern](https://gwern.net/note/fully-connected); TL;DR: the community moved on from FC nets before a lot of modern techniques (mostly, normalization and skip connections) were invented, so plausibly FC nets would be good now. Note that the NeRF model was an FC net.
- [FNet](https://arxiv.org/abs/2105.03824) does the mixing with some kind of Fourier transform. The important thing is that it achieves a mixing while being computationally quick ("trains 80% faster"). Presumably there's something wrong with this or it'd be SoTA
- To a lesser extent, note that various variations on attention do work; this is weak evidence that there's nothing particular about attention that does work.
	- Although, given this, does the KV cache thing work in favor of attention? Maybe.

### Neural Architecture search?
https://www.reddit.com/r/MachineLearning/comments/179awrx/d_what_is_the_current_sota_of_neural_architecture/