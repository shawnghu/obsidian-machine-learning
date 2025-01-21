TO READ:
[Efficiently Scaling Transformer Inference](https://arxiv.org/abs/2211.05102)

# KV Cache
https://www.youtube.com/watch?v=80bIUggRJf4

https://medium.com/@plienhar/llm-inference-series-4-kv-caching-a-deeper-look-4ba9a77746c8

For some reason I thought this was QK cache for the longest time, but that doesn't really make sense.
"Queries" correspond to new tokens; "keys" correspond to whether our new token attends to those old tokens.
If you think about the structure of the computational graph for a transformer, nothing about the embeddings at any layer for any token depends on the embeddings at any layer for any tokens later in the sequence. That means that the entire forward pass for a given sequence remains exactly the same.  Furthermore, the only places where tokens interact is in the attention mechanism. That means if we simply store the result of the K and V matrices (i.e, W_K * embedding) at each layer, we have all we need to perform inference for the next token at any given time.

This makes the effective cost of computing a token O(ND), where N is sequence length and D is embedding dimensionality. (Computing a sequence of N tokens is still O(N^2D), though.)

This cache also takes O(ND) in memory, and is the reason that people say that transformer inference is memory I/O bound instead of compute bound.
It's possible to make tradeoffs with inference time and also precision in various ways; this is a motivation for quantization of activations (and not just weights).

**This trick only really applies to inference time. If you think about the training procedure, you get a bunch of training samples out of one sequence already, so you have to compute the embeddings for every token anyway.**

### Cache invalidation?
One concern I had was: if a token is pushed all the way outside of the context window, this *will* actually have an effect on the embeddings of all the tokens in the sequence, no? And then this will invalidate the entire cache?

This would be true, but one misconception I had was that the maximum sequence length was a property of the model, because that's how the naive implementations I had seen worked. But actually, there's nothing in the description of the computations that requires us to hardcode a sequence length, and so this  (Actually there's the positional embeddings- if the positional embeddings are e.g sinusoidal, and the model never saw anything with an embedding for a position greater than 2048, then it might not really know what to do with that embedding and performance would degrade. But we can get out of this with cleverer embedding schemes.)

### Limitations to length anyway
Limits to total memory due to the size of the KV cache is one of the major limiting factors for context length if attention is implemented in the standard way. Much research goes into working around this limitation.
Some ideas include:
- **Multi-query Attention**, where multiple query heads will share a single key/value, so that the 
- quantization, which provides a constant multiple improvement;
- some sort of state machines, which compress tokens beyond a certain range into some other representation, analogous to an RNN;
	- see also sliding-window attention, where tokens simply aren't able to attend to tokens beyond a certain range, so you can forget the cache beyond a certain distance
	- arguably RAG is a variation of, or addendum to this; if your state just has you intelligently look at another part of your context which you've chosen to forget, and you think of your database as just an extremely long context, then there you go.
	- the boundary between this and different attention implementations or straight up different architectures is large.
- straight up forgetting a bunch of tokens/key values, because tokens didn't attend to them anyway;
	- a slightly more advanced variation, exploiting sparsity in the attention pattern generally.
This all goes deeper when you try to optimize a cache for a specific engineering purpose, like keeping around a KV cache when your chatbot's user leaves the conversation indefinitely. Strategies for this are IMO more appropriately generically the domain of classical CS/engineering stuff, like managing and not fragmenting memory, cache policies, etc.

### Sharding considerations
I don't really want to write about this, but more to note that these exist. Generally for inference you're sharding the KV cache across GPUs. I have no idea why the medium link mentions sharding across batch size; I would think that would be free to do.

https://medium.com/@plienhar/llm-inference-series-5-dissecting-model-performance-6144aa93168f

# Alternative Positional Embeddings
### Rotary positional embeddings


# Quantization
