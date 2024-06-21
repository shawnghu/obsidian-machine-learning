---
tags:
  - ConceptualSummaries
---
## GloVe

## Word2Vec
https://arxiv.org/pdf/1301.3781
An early vector embedding model, developed at Google in 2013; SoTA when it came out
- only works on words in a predefined vocabulary
- historically one of the first things to take advantage of large corpora of unstructured text in the billions of words as "labels"
- observation: it helps to increase vector dimensionality not only when your dictionary increases, but also when your corpus gets larger (more dimensions capture more subtleties)
### Skip-gram
- Makes a big assumption, that word vectors should be close to the word vectors of their neighbors (obviously this isn't generally true, but also this clearly averages out well enough)
- The other assumptions can be summarized as follows: *we want to maximize the total probability for the corpus, as seen by a probability model that uses words to predict its word neighbors* (Wikipedia)
	- This is to say, for a given example, where the middle word is missing, the word neighbors are the "labeled datapoints" and we are trying to fit the parameters of a model that should put the correct word in the missing spot (but instead predicts a probability distribution over the words that could go in that spot).
	- The "score"/logit associated with a (word, neighbor) pair is just the dot product of their vectors, and so the logit associated with a word is the sum/average of these dot products.
		- And then the loss is just the cross entropy loss, so we're maximizing the log-likelihood: we take the logit for each word and then do a softmax over all logits
		- Observe that actually calculating the cross-entropy here means performing a softmax so that you can normalize the probability of a given label.
			- Note this is actually computationally infeasible, since the normalization means calculating the sum over all words in the dictionary of $e^{logit}$.
			- So in practice people will pull computational tricks like "hierarchical softmax".
			- Or negative sampling, instead of taking the sum over the entire corpus, just take the sum over several random words.
		- Also observe that minimizing cross-entropy loss corresponds to maximizing the dot product of the vectors we're trying to push together (modulo some normalization) + minimizing the dot product of vectors we're trying to push apart (also modulo some normalization).
			- Is there an easier algorithm we could use, then?
				- Seems like we could just try to put upward pressure (ie, assert that the gradient is positive, eg by taking the difference with a large negative number as the loss) on the dot product directly.
		

### Continuous Bag of Words (CBOW) method
- Morally similar, but just use the word to predict the neighbors instead
- Makes the same essential assumption, drag the word vector towards the average of all the sums
- Apparently this is faster to train but performs less well on rare words compared to skip-gram
- To restate the modeling assumptions, for a given example, the word is the "labeled" datapoints and we are trying to fit the parameters of a model that should predict all the context words (or "equivalently" given our assumptions, their average).
	- And as before, the "closeness" is just the dot product, so we try to upweight (dot product of average of context words, true center word), and we try to downweight (dot product of average of context words, every other word).
		- I think this should be amenable to negative sampling as well; Wikipedia just says "numerical approximation tricks".

### Extensions
Actually the paper presents these in the reverse order, i.e, these are the core result and the way we actually produced the good word vectors, and the above two methods are linear "simplifications". Actually-actually, they say what works best is to pretrain the embedding vectors with the linear method and then "fine-tune" it with the NN.
But actually, just take the mappings above and replace them with two layer neural networks which map the "input" (in their original wording, some projection of the last few words onto a 500-vector) to a set of logits (one for every possible word).

- They mention `avoiding normalized models completely by using models that are not normalized during training` to save compute, which sounds a lot like my "put upward pressure on the dot product" idea
- They also try some RNN thing which I am not interested in, which seems like a sort of throw-in experiment since I don't think it's on their results table and it appears to be a vanilla RNN (it was 2013).
- Also observe that in the above setups you can make a distinction between the vector for a word when a word is used as context, vs when a word is the "center" word, ending up with two distinct embeddings of the dictionary. You could use one or the other or average them; I favor making the two representations the same in the first place.

## Word embeddings with Noise Contrastive Estimation
https://proceedings.neurips.cc/paper/2013/file/db2b4182156b2f1f817860ac9f409ad7-Paper.pdf (by DeepMind, 2013)

- At its core, it's a method which tries to avoid the softmax computational problem mentioned for word2vec.
- This paper also mentions that another really common way of modeling words is to predict them from the past context in some way.
	- Giving up the bag of words model and instead modeling sequential structure naturally leads to an RNN language model, which is something people did back then
- But anyway, this paper again tries to use linear models to take advantage of a corpus of ~billions.
### Noise Contrastive Estimation
- So we're again trying to avoid the softmax problem and end up with a parameter update that can be computed in time which does not depend on the vocabulary size
- NCE is called this because we setup a "noise" distribution, and try to "contrast" the examples drawn from our dataset from those drawn from the noise distribution.
	- `We are free to choose any noise distribution that is easy to sample from and compute probabilities under, and that does not assign zero probability to any word. We will use the (global) unigram distribution of the training data as the noise distribution, a choice that is known to work well for training language models.`
- This feels to me to be about the exact same thing as negative sampling above, where the proportion of noise samples corresponds to the number of negative samples used in the word2vec setting (and we weight by unigram distribution).
## Triplet Loss



## Deep contextualized word representations
https://arxiv.org/abs/1802.05365

## Connections to modern tokenization methods