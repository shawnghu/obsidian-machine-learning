*Core question: How, on an engineering level, is it possible to make a ChatGPT which takes in image data as part of the user prompt, and then does something actionable about it?*

(The question can naturally be extended to video or audio.)

It's already clear as a premise that you can embed images in a joint image-text space using methods similar to those of [[CLIP]]. But this method doesn't by itself seem to be sophisticated enough to handle fine details or general composition in images. I doubt this is the kind of thing that can be solved by a massive amount of data, especially with the naive captioning approach that CLIP uses.
For example, Claude was able to interpret diagrams about circuit wiring which also contained a lot of text. Maybe if there were more text and the location of the text were more important, its performance would degrade.

Another basic question: are OCR capabilities automatically learned?

[PaLI](https://storage.googleapis.com/gweb-research2023-media/pubtools/6788.pdf), by Google

- used a pretrained language model and pretrained image model
- text model was based on T5, not sure what that is yet
- image model was the largest vision transformer to date at the time, 4B params
	- 
	- after performance saturated on known benchmarks like ImageNet vision-language performance continued to improve, following classic scaling intuitions
- they do the simplest thing you can think of: `To include vision as input, the text encoder is fed with a sequence of visual “tokens”: output features of a Vision Transformer which takes as input an image.`
- It seems that the weights are not frozen and pretraining just consists of a bunch of tasks that span a mixture of text only and image 
- This particular model is constrained to only produce text tokens, and is trained in what seems like the same general way most autoregressive LLMs are. (In principle it should be possible to generate)

[Florence-2](https://arxiv.org/pdf/2311.06242) , by Microsoft, seems to promise to answer a lot of the task complexity questions by having highly structured input data.