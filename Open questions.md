[[Training language models to follow instructions with human feedback||RLHF]]
- https://captum.ai/docs/introduction.html
	- Integrated gradients:
		- https://arxiv.org/abs/1703.01365
		- https://www.youtube.com/watch?v=MB8KYX5UzKw
- transformer interpretability beyond attention visualization https://github.com/hila-chefer/Transformer-Explainability
- [Backward Feature Correction: How Deep Learning Performs Deep (Hierarchical) Learning](https://arxiv.org/abs/2001.04413)
- [Adversarial Examples Are Not Bugs, They Are Features](https://arxiv.org/abs/1905.02175)
- [ Hopfield Networks is All You Need (Paper Explained) ](https://www.youtube.com/watch?v=nv6oFDp6rNQ)
- [The Many Faces of Robustness: A Critical Analysis of Out-of-Distribution Generalization](https://arxiv.org/abs/2006.16241)
- https://thezvi.substack.com/p/on-anthropics-sleeper-agents-paper
- [The Hydra Effect: Emergent Self-repair in Language Model Computations](https://arxiv.org/abs/2307.15771) (only like 30 citations; Google DeepMind)
- [What Would Jiminy Cricket Do? Towards Agents That Behave Morally](https://arxiv.org/abs/2110.13136) (how are they gonna define "morally" with this one?)
- [Incentivizing High-Quality Content in Online Recommender Systems](https://arxiv.org/abs/2306.07479) (how are they gonna define "quality"?)
- https://www.lesswrong.com/posts/ZHrpjDc3CepSeeBuE/gpt-3-a-disappointing-paper and https://generative.ink/posts/language-models-are-0-shot-interpreters/
- [The Effects of Reward Misspecification: Mapping and Mitigating Misaligned Models](https://arxiv.org/abs/2201.03544)
- [Direct Preference Optimization: Your Language Model is Secretly a Reward Model](https://arxiv.org/abs/2305.18290)
- [Scalable Extraction of Training Data from (Production) Language Models](https://arxiv.org/pdf/2311.17035)
- [Elephant Neural Networks: Born to Be a Continual Learner](https://arxiv.org/abs/2310.01365) (but only one citation, seems promising so just give it a small try)
- https://sites.google.com/view/multi-game-transformers
- [Representation Engineering: A Top-Down Approach to AI Transparency](https://arxiv.org/abs/2310.01405)

- Rademacher complexity
- Kolmogorov complexity
- Information theory, again
- llama adapter and adapters generally
- lora/low rank adaptation

- extra mathematical justification for softmax?
- Review word embedding stuff-- how are they calculated again? [link](Word Embeddings)

- Think critically: why should regularization actually prevent overfitting?
- [x] Review attention
	- [x] Attention is all you need was the first transformer?  *yes*
	- any relevance to self vs cross attention? which was invented first?
	- what was the first attention paper?
- Read into some basic transformer stuff
- [x]  what is BERT specifically?
	- [ ] it's a model trained by google that was SOTA back then, popular, encoder only
- How do you go from having a working transformer to having a sort of chatbot thing?
- How do multimodal architectures work?
- How to change context size, or generally input size to a model?
- In GPT-3 specifically, why use such a high-dimensional space (~12k) to embed something like only ~50k words? *this is not an easy question to find the answer to, need to actively ask on e.g stackexchange or ML reddit*
	- Do they have a paper? *yes*
- Furthermore, what is the purpose of the fully connected layers and are they necessary? *i bet that they are necessary but otherwise this is not easily answered; waiting on 3b1b's video on it*

### Some quick clarifications

- [x] How does HuggingFace work? Can you download models straight? *yes*
- [x] Phrased differently, maybe this is the right question, where can I just "get" a pre-trained BERT model? *yes, by specifying to the API by string keyname*

- [x] How do people work with TPUs, and what is a TPU exactly? *i no longer think this is important; tpu isn't anything specific but rather just a chip type manufactured by google, and as a general matter i'm pretty sure people work with them by just setting the compute setting in pytorch and hopying things go faster*
- [x] pytorch lightning *it's just a lib, supposedly for deep learning researchers to improve flexibility. hard to say whether it's worth anything but it seems well supported*
how do notebooks work; how is the kernel separated from other stuff and what conceptually is a standalone kernel, in detail?
what is palm?
how do generative models work these days?
what is diffusion?
nerf
neural ode

what does it tkae to make a chatbot out of a working decoder-transformer? https://openai.com/index/chatgpt/
https://arxiv.org/abs/2203.02155

how to construct adversarial examples
style transfer
what is a fully convolutional network

[x] what is a gabor filter *it's something from classical vision that basically detects patterns with a frequency in a direction*
[x] is adam still the main optimizer or did anything change in optimization theory *nope it's still basically the same*
[x] same with batch normalization *a little bit antiquated/disfavored for various fundamental reasons*
[x] , resnets *still considered broadly important; found in the base transformer architecture*
[ ] more generally, are there new methods for training particularly deep networks that are still broadly relevant
[x] 1x1 convolution *used to reduce (or increase) the number of channels*
matrix factorization relevance

deep double descent
lora
learn how to use huggingface from public repos as examples
...how do i get people to do this work with?

[x] encoder/decoder networks *loose terminology, often confused for the tasks that they are actually used for because decoder-onlys like GPT are often used for autoregressive sequence generation. Also a decoder-only does encoding, so it's a bad name*
[x] attention for sequence data *supersedes rnns, otherwise the application is fairly obvious and is the default case*
[x] attention for image data
[x] rnns for image data
[x] cnns for sequence data
lstm has hidden state and cell state

transformer xl (transformer with recurrent stuff)
[x] attention is all you need paper *read*
linear probing (mech interp)
pre-ln (layer normalization)

multiplication by a low rank matrix (saves parameters because it can be factored into smaller matrices, but how bad is this for statistical expressiveness?)

scaling laws evidence
prompt engineering as a skill
gpt1 paper https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf
[x] gpt2 paper
gpt3 paper
gelu paper https://arxiv.org/abs/1606.08415

https://arxiv.org/abs/2404.13208

torch compile
torch forward hooks underneath `__call__`
does forward() need to be defined for training to function?
torch eval()

improving performance on a dataset by pretraining on differently structured data (e.g, char level transformer on shakespeare)
	- you can numerically measure this with a validation set

quantization, NAS, distillation of neural networks
IR in the context of machine learning optimization (Triton, HLO, MILR, Relay)

how to stop and start pytorch kernel for rapid debugging? is it possible?

https://github.com/openai/transformer-debugger

- Gshard and XLA compiler https://arxiv.org/pdf/2006.16668
	- The English in this paper isn't that good.
	- Trains a model with 600 billionparams on 2048 TPU accelerators in 4 days
		- Fundamentally sort of a systems technology, coordinating the computation across devices