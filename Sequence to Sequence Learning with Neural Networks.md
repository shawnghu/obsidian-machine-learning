https://arxiv.org/pdf/1409.3215
Google: Sutskever, Vinyals, Quoc Le
Dec 2014
The first neural machine translation system that outperformed a phrase-based statistical machine translation baseline on a large scale problem
Unofficial but good looking implementation: https://github.com/bentrevett/pytorch-seq2seq/blob/main/1%20-%20Sequence%20to%20Sequence%20Learning%20with%20Neural%20Networks.ipynb

- The "classic" RNN machine translation baseline: put everything into a vector with encoding parameters, decode everything out of it with decoding parameters
- This paper shows obvious returns to scale and not that many diminishing returns. It seems based on the context that they just didn't find it practical to use more than 8 GPUs, and beyond that there are probably computational tricks that they missed to make it faster. But this exact approach probably could have been made much stronger simply with more compute.
- 