is not nearly as complicated as I thought it might be.

You basically just declare that when tokens adhering to a specific structured format are observed by an orchestrating program, the program will make a call to an external tool and pass the output to the LLM (with context as necessary). Then you (train the model) (this phrase is doing a ton of work here, but also that's how deep learning is) at some point in the pipeline, probably before the final RLHF, with the assumption that this is the way things work.
[ReAct](https://arxiv.org/pdf/2210.03629)