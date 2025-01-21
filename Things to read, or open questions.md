sleeper agents
model organisms

callum's thing
mixture of experts models
rlhf
inverse scaling

is context length fixed?

what is integrated gradients?
what is attribution patching?

what is instruction tuning?


[Constitutional AI: Harmlessness from AI Feedback](https://arxiv.org/abs/2212.08073)
[Bag of Tricks for Image Classification with Convolutional Neural Networks, AKA Resnet-D](https://arxiv.org/pdf/1812.01187)
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
- https://www.lesswrong.com/posts/ZHrpjDc3CepSeeBuE/gpt-3-a-disappointing-paper by nostalgebraist, the logit lens guy: highly critical, doesn't disparage the fact that more params is good but does not like the emphasis on "few shot learning" because he feels that this paper doesn't demonstrate much useful about it; strange that it does not put more emphasis on the task of "using novel words".
	- this gives me an idea: what happens if you try to ask an LLM to switch the meanings of two well known symbols, e.g, "+" and "-" (then ask, what is "3 + 2" expecting "1")?
		- i tried this, it works sometimes and sometimes does not work
	- and https://generative.ink/posts/language-models-are-0-shot-interpreters/
- [The Effects of Reward Misspecification: Mapping and Mitigating Misaligned Models](https://arxiv.org/abs/2201.03544)
- [Direct Preference Optimization: Your Language Model is Secretly a Reward Model](https://arxiv.org/abs/2305.18290)
- [Scalable Extraction of Training Data from (Production) Language Models](https://arxiv.org/pdf/2311.17035)
- [Elephant Neural Networks: Born to Be a Continual Learner](https://arxiv.org/abs/2310.01365) (but only one citation, seems promising so just give it a small try)
- https://sites.google.com/view/multi-game-transformers
- [Representation Engineering: A Top-Down Approach to AI Transparency](https://arxiv.org/abs/2310.01405)

-  On the geometry of generalization and memorization in deep neural networks
- https://arxiv.org/pdf/2206.04301
- 2023 Look Before You Leap: A Universal Emergent Decomposition of Retrieval Tasks in Language Models
- 2024 Fine-Tuning Enhances Existing Mechanisms
- 2024 How do Language Models Bind Entities in Context?

There is a lot to understand about the dynamics of fine tuning:
	- You can see the pretraining step as a sort of meta optimization and the fine tuning as the true optimization.
		- Note that with respect to the fine tuning data, models are often severely overparameterized, and in this context now can think of the pretraining as introducing "implicit" biases for the fine tuned task.
		- 
	- Also for transformers there is "in context learning" to consider, which is not the same thing but complicates the matter of tracing the source of certain outputs.


- Sharding: Gshard and XLA compiler https://arxiv.org/pdf/2006.16668
	- The English in this paper isn't that good.
	- Trains a model with 600 billionparams on 2048 TPU accelerators in 4 days
		- Fundamentally sort of a systems technology, coordinating the computation across devices
- Rademacher complexity
- Kolmogorov complexity
- Information theory, again
- llama adapter and adapters generally
- lora/low rank adaptation


- Review word embedding stuff-- how are they calculated again? [link](Word Embeddings)

- Think critically: why should regularization actually prevent overfitting?
- 
- How do you go from having a working transformer to having a sort of chatbot thing?
- How do multimodal architectures work?


### Some quick clarifications

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


deep double descent

[x] attention for image data
[x] rnns for image data
[x] cnns for sequence data

transformer xl (transformer with recurrent stuff)

scaling laws evidence
prompt engineering as a skill
gelu paper https://arxiv.org/abs/1606.08415

https://arxiv.org/abs/2404.13208

improving performance on a dataset by pretraining on differently structured data (e.g, char level transformer on shakespeare)
	- you can numerically measure this with a validation set

quantization, NAS, distillation of neural networks
IR in the context of machine learning optimization (Triton, HLO, MILR, Relay)

https://github.com/openai/transformer-debugger
