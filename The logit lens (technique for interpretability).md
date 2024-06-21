---
tags:
  - Papers
  - ConceptualSummaries
---
- [ ] [link](https://www.lesswrong.com/posts/AcKRB8wDpdaN6v6ru/interpreting-gpt-the-logit-lens#logits)

- The core idea: 
	- The outputs of the transformer blocks are all the same dimension.
	- This is the same as the dimension of the input.
	- The output of the last block is mapped directly to the logits by a linear transformation.
		- For the purposes of this study, that LT is just the transpose of the embedding matrix, which is what GPT2 does (though not all transformer implementations do, but this is considerably more interpretable)
			- Linear algebra interpretation: what does the transpose do? well, the word with index 1 is going to map to some column vector, and that vector is going to have really high dot product with the first row of the transpose (since they go in exactly the same direction). So it's kind of like an inverse, in that it maps the embedding of vector 1 to something with a strong component in the 1-direction.
	- So, you can try to just interpret the outputs of any intermediate block as if they were the outputs of the last block, and apply that same linear transformation as above to these outputs, to see what happens.
		- This idea generally works and gives some interpretable output
		- Several notable observations include:
			- You may expect the result of blocks near the beginning to resemble the input, since you've just embedded and unembedded your input sequence. But the very first transformer block scrambles things strongly so that they are more like (as measured by KL divergence) a very crude estimation of the output.
				- This is actually kind of surprising, since vageuly speaking, L2 reg/weight decay should incentivize small transformations in each block.
		- Note that the fact that these are residual networks means that we are likely to represent the same vectors w.r.t the same basis, which helps us view these logits in the way that we do.
		- He also does a study on how repetition works, using this prompt : *Sometimes, when people say plasma, they mean a state of matter. Other times, when people say plasma* 
			- Note that plasma is a really rare token, so you have to know the structure in order to predict plasma
			- One hypothesis is that early attention layers may have learned to recognize the repetition, then to "copy over" the values corresponding to the word "plasma" to the last word in the sequence.
				- This hypothesis seems completely false, and somehow instead the later layers just reconstruct the word "plasma" from scratch.
				- This also holds for the extreme example where the sequence looks like "i love plasma i love plasma ... "
		- 
## The extension notebook
[link](https://colab.research.google.com/drive/1MjdfK2srcerLrAJDRaJQKO0sUiZ-hQtA?usp=sharing#scrollTo=6KccW-jtzXVs)
- Uses mostly the same utilities to explore other models, plus a couple of other observations about MLP and "extended decoder"

Copying his summary mostly, 
- gpt-neo models (125M, 1.3b, which is about the same size as gpt2, and 2.7b) behave considerably differently: taking outputs of earlier layers and interpreting them as logits is useless all the way up to the MLP of the final layer
	- However, taking the last transformer block of the model, and thinking of it as part of the "decoder", ie, the "lens" through which we interpret these vectors, gives us something better.
		- This requires using the entire transformer block, not just the MLP.
- CTRL models behave much like GPT2, where interpreting the logits does something useful
	- In addition to this, it exhibits an even nicer behavior, where the early logits look like the input, and it smoothly transitions into looking more like the output, like some may have originally expected.

