

(typical supervised learning setup with e.g FC NN assumed) When we talk about minimizing the objective function, I realized people usually aren't that clear about what the dimensions of the "objective landscape" represent. Let n be the dimension of the input and p the number of parameters in the model.
- In the first place, it seems like what we really want to find is the function on n variables which predicts the label. Our dataset consists of a series of points which sketch out the skeleton of this function, however imperfectly, and the ideal model will fit just well enough to draw out the actual function.
- But usually we perform optimization on our p parameters in p-dimensional space. Points in this space correspond to functions on n variables
- The loss implicitly comes from our divergence from the ideal function, or in terms of the training process, the loss for each set of parameters is actually computed from the training data points.
- The bottom line question is: What is the relationship between the n-dimensional space and the p-dimensional space? 
	- I guess the question is a little tautological because the loss function actually characterizes the relationship, but still, are there other ways of envisioning this, or deriving unusual insight from these basic observations?