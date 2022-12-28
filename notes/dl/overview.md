# Neural Networks

- network can be viewed as a function we want to learn that perfectly maps from inputs to outputs
    - given a dataset, how we define our loss function determines how well we learn the mapping (how well we approximate the function)
- logistic regression can be seen as a special instance of a neural network
- A neuron is an operation that is a composite of a *linear* operation with an *activation/thresholding* operation
    - Classification Tasks:
        - Neurons in early layers of a network become feature detectors for things such as edges
            - 1st layer can only detect edges or similar basic features since it is given only pixel information in a simple fully connected network  
            - later layers can detect more complex features by combining information from earlier feature detectors indicating the presence/orientation of certain edges or other simple features
        - Neurons in the later layers build up more complex feature detectors using the feature detector neurons in the previous layer and the weights connecting the layers 
    - Regression Tasks:
        - Layers learn more complex features from the input features (e.g. relationships between features, the weighting of importance of certain features)
        - The learned features are often better than hand engineered features
            - Often difficult to understand what features are being learned and that's why NN's are often considered black boxes
- A model is an *architecture* with *parameters*
- *end-to-end* learning- we train based on inputs and outputs and don't care about whats happening on the inside (blackbox model) 
- Loss Function $\mathcal{L}$- for 1 example
- Cost Function $J$- for multiple examples
    - $J = \frac{1}{m}\sum_{i=1}^m \mathcal{L}^{(i)}$
    - Can find the derivative by just computing derivative of $\mathcal{L}$ since summation is a linear operation so we can just compute the derivative inside the summation
- Normalizing input to neural networks can help it learn better since certain features will not have outsized influence due to their scaling/units
    - normalize = center (subtract by mean) and standardize (divide by std deviation)
    - this results in circular contours to the cost function which result in a smoother descent for gradient descent compared to the unnormalized input which will have ellipsoidal contours
    - mean and standard deviation from the train set must also be applied to test set
- Smaller the batch, the more noisy the convergence
    - Full batch is the best approximation of the true cost function
    - Smaller batches serve as good enough approximations of the true cost function that are faster to compute, allowing more updates to the parameters in a given amount of time
    - More (less accurate) updates are typically preferred over fewer (very accurate) updates
        - the most accurate updates computed over the whole batch will have the smoothest convergence
    - Some research suggests the stochastity of smaller batches/single samples in gradient descent can help it escape local minima in the cost function that full batch gradient might get caught in

## Weight Initialization

- One way to avoid vanishing and exploding gradients is by initializing the weights to be near the ideal values
- The larger the number of input features to a layer, the smaller we want each individual weight to be so that the dot product of $w^Tx$ does not explode/become too lare
    - For sigmoid activation an initialization that works well: $w^{[\ell] } = \text{random}(shape) \times \frac{1}{\sqrt{n^{[\ell - 1]}}}$
    - For ReLU activation an initialization that works well: $w^{[\ell] } = \text{random}(shape) \times \frac{2}{\sqrt{n^{[\ell - 1]}}}$
- Xavier Initialization 
    - used for sigmoid and tanh activation
    - [Read More](https://cs230.stanford.edu/section/4/)
- He Initialization:
    - used for relu activation
    - takes into account number of inputs and outputs b/c of the back propagation step 
- Weights need to be randomly initialized or else network will suffer from the symmetry problem where all neurons start learning the same thing (need to be able to evolve independently)

## Training Tips

- [Karpathy's NN Training Recipe](http://karpathy.github.io/2019/04/25/recipe/)
- **understand your data inside out**
    - spend hours looking through examples and determining patterns or corruption in the data 
    - imbalances 
    - biases
    - your process of classifying the data (hints at architecutre needed)
    - understand the form of the variation and if it can be preprocessed out (e.g. remove the x, y variation in the initial state for all the trajectories to reduce amount of variation that has to be learned over)
    - viz the data as many ways as possible and watch out for outliers
- **setup training/eval skeleton and get dumb baselines**
    - simplest model possible
    - fix random seed to remove a factor of variation and help with debugging
    - simplify (e.g. no data augmentation, dropout, bath norm, etc.)
    - initialize the network well
        - verify the loss starts at correct value
        - set the biases to eliminate hockey-stick loss curves
    - overfit to one batch
        - batch should be small like 1 or two samples
        - verfiy the outputs match the targets when loss driven to 0 (otherwise there is a bug somewhere)
    - vizualize the inputs to the neural network right before being passed in to ensure no bugs with data preprocessing/augmentation
    - visualize model predictions on a fixed test batch over the course of training
        - lets you see the dynamics of how the predictions are moving -> good intuition for how training is progressing
    - instead of starting with very general code, write for a specific case, make sure it works, and then generalize if needed (making sure you still get the same result)
        - ex: write out loopy version first before vectorizing
- **overfit**
    - find a large enough model to overfit the dataset (only focus on driving down the training loss)
        - if no model seems to be able to reach low error rate, something is amiss
    - then regularize it appropriately (give up some training loss to improve validation/test loss)
    - when picking the model go with the simplest possible architecture first and improve from there
    - start with Adam with $\alpha = 3e-4$
    - build up complexity little by little
        - don't start with all the features available for tabular data, instead start with small subsets and add features one by one, verifying they give the performance boost one would expect
        - don't immediatley go for the highest quality input images, instead start with lowest quality images as input and verify whether the higher quality images do boost performance
    - don't trust learning rate decay defaults (schedule depends greatly on the problem since oftentimes based on current epoch number so can be sent to 0 too early)
        - best practice to turn off learning rate decay and use constant learning rate (can tune this at very end of project if necesary to squeeze a boost)
- **regularize**- we have a large model that is well fit to the train set so now we regularize it to improve validation score
    - get more data is always the best way to do it
        - data augmentation can be used
    - ensembles can be good but tops out at ~5 models
    - pretrained networks are nice places to start if available
    - reduce dimensionality of input if possible since it just makes it easier to overfit with not enough data for the dimensionality
    - can make models smaller by using problem domain knowledge as constraints on the network
    - decrease batch size if using batch norm in your network
    - can add droopout but watch out b/c it doesn't work well with batch norm
    - early stopping- stop based on validation loss (is technically leaking validation data into training but its still commonly used)
    - increase weight decay penalty
    - visualizing the activations in the network can sometimes help show when something is wrong
- ensembles can basically increase 2% accuracy on anything at the cost of the extra training/compute time



## interesting

- ImageNet and Alexnet and others can simply be treated as feature extractors on imgs where the learned features are sensitive to semantic concepts while remaining invariant to nuisance/uninteresting variables such as appearance and lighting 
- trained neural networks can be used in cost functions and are useful since they are differentiable with respect to their input