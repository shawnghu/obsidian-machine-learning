Short summary of their method:
Get two pretrained LMs, one generally weaker than the other
Finetune the weak one on a task with some ground truth labels
Finetune the strong one on the outputs of the weak one (as if the weak one is teaching the strong one how to do the task)
We hope that the strong one will learn how to do the task in generality from the demonstrations, and measure how close we can get the performance of the strong model to its performance when just finetuned directly. Much of the paper is dedicated to measuring the baseline performance when doing this and coming up with ways to increase the portion of performance gap recovered.


## An alternative experimental setting
In my understanding, a lot of this experiment relies on the setting where we begin with two *pretrained* models. Unless I'm mistaken, if you took two untrained models, trained a weaker one to do a task, and trained a stronger one on the weaker one's labels, the "stronger" one's performance is probably upper bounded by the weaker one's. (Maybe not, though.)
Maybe the stronger one just generalizes due to some biases inherent to its structure/the problem, or maybe this generalization only happens when you "start" from a position where you have all the pretrained biases built in.
In this case, finetuning specifically as a method of learning the data is also kinda weird, but I guess I don't know what other methods are possible.
	- Ah, they're aware of this too, that's why they do these prompting experiments.
	- One possible story is, it's easy for the strong models to "fit" the new task because they reflect something it "already knows". In order to test this hypothesis we try to elicit its knowledge of the task via prompting.

They are aware of this fact: 
```
These results suggest that pretrained models may have a hard time fitting errors of other (smaller)
pretrained models, at least in finetuning settings with relatively limited data. Stanton et al. (2021)
and Furlanello et al. (2018) report a related observation in the context of knowledge distillation: it
is surprisingly hard for models to fit the predictions of other models, even when they have sufficient
capacity to do so.
```


### Task saliency
If you finetune the model to just complete text which is examples of your task, whether they are positive or negative examples, it becomes better at actually performing your task, because the task "becomes more salient" or "has more salient representations of the task". Intuitive but definitely not obvious that this would happen. (This is unstated, but surely you have to do this before finetuning on the labeled examples?)

### Linear probing
They do some linear probes on the strong model after training it on the "weak" labels and the "ground truth" labels. They also compare the results of training the probe with respect to the weak labels and the ground truth labels.
They find the strange result that finetuning on the weak labels improves the linear probe relative to ground truth labels substantially, and conjecture that this effect could generalize, which would be nice

# General objections to the methodology
Nostalgebraist's objection, which I also felt but didn't articulate as well as him:
Why do we want this, exactly?
So to play OpenAI's advocate, imagine there is some platonically correct notion of "ethical behavior" or "human values" that we are just sort of noisily approximating / we can't perfectly well answer questions about. Then we're just "demonstrating human values" and a strong AI can recover human values better than our demonstration can.

However, on the flipside, the strong models *are judged to be good when they do something other than what the weak models demonstrate*. 

Further objections, even if we do want it to generalize beyond our behavior, why are we trying to demonstrate human values to superintelligences by giving it examples of our general low-level behavior anyway? We often want to train a superintelligence in situations where we don't know what the right low-level behavior is in the first place. (In other words, this is a serious weakness of the preference annotation aspect of the experiment design.)

