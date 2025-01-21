My reflex when I see a bunch of papers that demonstrate the ability to make a model say bad things is: so what?

spitballing: all of these things are sort of red-teaming for the capability we really want to exercise, which is control over model outputs. If we knew scientifically how to control model outputs in such a way that the model couldn't be effectively jailbroken, then we'd be somewhere significant with respect to alignment. In this view, individual model attacks are important in that they shed some kind of light on the weaknesses of our current schemes for engineering model output. (By contrast, AFAICT the direct effects of doing this for most LLMs/chatbots matter a lot less. It doesn't really matter if ChatGPT tells you how to make a bomb.) 

This perspective holds even more strongly when you talk about attacks that are possible when you fine-tune the model, or have some access to its dataset: well, yeah, given that level of control over a model you can really make it do anything, can't you? Nevertheless there are some empirical insights that are sort of training dynamics-flavored:
- A small amount of finetuning seems to be able to undo safety training (i.e, more evidence that existing safety training is brittle).
- Even a small amount of data poisoning may open an attack surface (this is a signal about how much control you actually need to exert over the model to have the practical level of control you're interested in, i.e, an impractically high amount)



By contrast, what would be more important to observe/study?
- Deception/inner misalignment capabilities (this is a lot of work to operationalize also)
- Evals, i.e, measurement of general capabilities 
- Interpretability? So that we can apply human judgment, I guess?
- General politics, policy, that sort of thing? (painfully confusing, hard to tell the sign of impact; how would I start?)


I have some loose intuition that jailbreaking happens when things are out of distribution.

Another remark: Seems that models are intrinsically somewhat nondeterministic. Temperature seems to be intentionally nonzero, and also there are matters like distributed inference and floating point op orders.

[Best of N Jailbreaking](https://arxiv.org/abs/2412.03556): sampling a ton of small perturbations to a malicious prompt eventually works; the perturbations are simple/mundane things like capitalizing random letters or misspelling things. Intuitively, this increases the "entropy" of the input, and you'll find an attackable point. Just using this as a baseline, we can establish that whatever defenses we have are pretty poor from a certain perspective.

[Many-shot jailbreaking](https://www.anthropic.com/research/many-shot-jailbreaking): putting a bunch of demonstrations of malicious behavior in the prompt increases likelihood of getting malicious behavior when you e.g ask a question the model isn't supposed to answer. This seems to accord with a lot more general understanding of in-context learning (following the same scaling laws where performance improves w.r.t the number of examples, just with malicious tasks instead of benign ones). Also, this weakness persists even if you try to fine-tune it away, even in fairly specific and targeted ways, up to RL (zero shot performance may decrease, but the general power law remains, so you can get a jailbreak with long enough context in principle).

Both of the above papers demonstrated that success follows a power law (w.r.t the variable of number of attempts in BoN, and number of prompt examples in many-shot). Why the emphasis on power laws? An attempt to establish a science about it, I think? They also both compose reasonably well with other attack strategies, whatever those are.



What's the question E.Perez asked me in November that I did such a bad job at? Something like "how would you jailbreak a black box text + image model"? I remember I correctly had intuition about jailbreaking and OOD, but didn't have many tricks for how to induce OOD behavior.

I cannot yet write these papers, even if I were to have the core idea about the experiments. But probably that's okay.

I feel that I'm supposed to have done more with the people I met at constellation, particularly the people who were visiting.

When you release your code, how likely is it that anyone else is actually going to look at it and collaborate?