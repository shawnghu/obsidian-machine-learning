https://openai.com/index/clip/
[Learning Transferable Visual Models From Natural Language Supervision](https://arxiv.org/abs/2103.00020)
`current approaches have several major problems: typical vision datasets are labor intensive and costly to create while teaching only a narrow set of visual concepts; standard vision models are good at one task and one task only, and require significant effort to adapt to a new task; and models that perform well on benchmarks have disappointingly poor performance on stress tests`.

`By design, the network can be instructed in natural language to perform a great variety of classification benchmarks, without directly optimizing for the benchmark’s performance, similar to the “[zero-shot(opens in a new window)](https://en.wikipedia.org/wiki/Zero-shot_learning)” capabilities of GPT-2 and GPT-3.`
## Approach
- From a data perspective, they take advantage again of the mass of pseudo-labeled data on the internet, which is a good and natural idea.
- They try this on 8 different models, 5 of which are ResNets and 3 of which are [[Transformers for Images||vision transformers]], which seems to have not been the completely obvious choice a priori. (To add context, vision transformers were new at the time.)
	- It seems based on others' references that vision transformers were better, naturally, and the best model is often called CLIP-ViT or just ViT (for **Vi**sion **T**ransformer.)
- `CLIP is pre-trained to predict if an image and a text snippet are paired together in its dataset`. 
	- It achieves this by end-to-end training a text representation model, again naturally using a transformer, and then the prediction strength/logit is just the dot product of the text representation and image representation.
	- In the end, it conceptually functions as a multi-class classifier on input (image) and output (text snippets).
		- `Given a batch of N (image, text) pairs, CLIP is trained to predict which of the N × N possible (image, text) pairings across a batch actually occurred. To do this, CLIP learns a multi-modal embedding space by jointly training an image encoder and text encoder to maximize the cosine similarity of the image and text embeddings of the N real pairs in the batch while minimizing the cosine similarity of the embeddings of the N2 − N incorrect pairings.
		- 
## Misc. Remarks
- `When a linear classifier is fitted on top of CLIP’s features [to the ImageNet training set], it improves CLIP’s accuracy on the ImageNet test set by almost 10%. However, this classifier does _no better_ on average across an evaluation suite of 7 other datasets measuring “robust” performance.` That's a very clean demonstration of the "cheating hypothesis".
- `In the end, our best performing CLIP model trains on 256 GPUs for 2 weeks which is similar to existing large scale image models.`
	- That's actually pretty achievable, a small company or even a single rich/enthusiastic hobbyist is able to achieve this. (okay maybe the hobbyist wouldn't really like to network the 256 GPUs, but suppose they did)
- `when evaluated on handwritten digits from the MNIST dataset, zero-shot CLIP only achieves 88% accuracy, well below the 99.75% of humans on the dataset.` Back in the day people used to say that humans were only 90-95% on MNIST. This always seemed a little bit stupid to me and like a sampling artifact that people were using dishonestly to make AI look more impressive. Refreshing to see a larger number being presented.

### Remaining question
It's not clear what you can do if you have a pre-existing pre-trained language model. It seems like the vision and language sub-models were jointly trained from scratch here.
Also, here the objective is associations between image and text, which is a nice demonstration. But suppose you want images as input data in a way that interleaves them with text, the way you'd want to be able to communicated with a person or chatbot? That's a different objective, and I'm not sure how to engineer that one (and from an intuitive perspective, how does OCR arise?)