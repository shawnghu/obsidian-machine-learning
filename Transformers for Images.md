---
tags:
  - ConceptualSummaries
  - Papers
---

## An Image Is Worth 16x16 Words: Transformers for Image Recognition at Scale
https://arxiv.org/pdf/2010.11929
Google Research/Brain, mid-2021

- A very nice overview of the SoTA between NLP and image processing in June 2021
- References:
	- [Non-local Neural Networks](https://arxiv.org/pdf/1711.07971) , applying self-attention to a CNN architecture in 2018
	- [Axial-DeepLab: Stand-Alone Axial-Attention for Panoptic Segmentation](https://arxiv.org/pdf/2003.07853), applying pure attention (and some computational optimizations for 2d attention) to replace convolutions entirely in 2020
- `When trained on mid-sized datasets such as ImageNet without strong regularization, these models yield modest accuracies of a few percentage points below ResNets of comparable size. This seemingly discouraging outcome may be expected: Transformers lack some of the inductive biases inherent to CNNs, such as translation equivariance and locality, and therefore do not generalize well when trained on insufficient amounts of data. However, the picture changes if the models are trained on larger datasets (14M-300M images). We find that large scale training trumps inductive bias.`
- They say, in so many words, that vision transformers should be theoretically more efficient, but cannot capture the advantages of modern hardware accelerators due to specific attention implementations, and propose to fix thiat.
- Much focus before this was placed on getting attention to be more scalable or computationally tractable.
### Method
is insane. Just cut an image into little patches, turn the patches into embeddings using a learned linear transformation, and lay the patches out in a sequence (adding also a learned positional embedding). Then let the representation of the image be the attended-to vector of one of the patches (in this case, they append a special token, with a learned embedding, at the start of the sequence, and then use that one) at the end of the transformer layers. Then you can do whatever you want with it, in the case of this paper, classification