# Convolutional Neural Networks

- [CS 231n (CNNs)](https://cs231n.github.io/convolutional-networks/#comp)
- [Convolutional Arithmetic Paper](https://arxiv.org/pdf/1603.07285.pdf), ([blog post](https://kvirajdatt.medium.com/calculating-output-dimensions-in-a-cnn-for-convolution-and-pooling-layers-with-keras-682960c73870))
- Standard convulational block: Conv -> ReLU -> MaxPool

## PyTorch

- Need to flatten the output of the last conv block in order to be fed to the linear layer that acts as the classifier over the rich features extracted using the CNN architecture

### Conv2D

- `torch.nn.Conv2D(2, 28, 3)`
- **in_channels** (int) – Number of channels in the input image
- **out_channels** (int) – Number of channels produced by the convolution
    - each are feature maps that detect certain key features
- **kernel_size** (int or tuple) – Size of the convolving kernel
    - can be square (int) or non-square (tuple)
- **stride** (int or tuple, optional) – Stride of the convolution. Default: 1
- **padding** (int or tuple, optional) – Zero-padding added to both sides of the input. Default: 0
- **padding_mode** (string, optional) – ‘zeros’, ‘reflect’, ‘replicate’ or ‘circular’. Default: ‘zeros’
- **dilation** (int or tuple, optional) – Spacing between kernel elements. Default: 1
- **groups** (int, optional) – Number of blocked connections from input channels to output channels. Default: 1
- **bias** (bool, optional) – If True, adds a learnable bias to the output. Default: True

### MaxPool2D

- **kernel_size** – the size of the window to take a max over
- **stride** – the stride of the window. Default value is `kernel_size`
- **padding** – implicit zero padding to be added on both sides
- **dilation** – a parameter that controls the stride of elements in the window
- **return_indices** – if `True`, will return the max indices along with the outputs. Useful for [`torch.nn.MaxUnpool2d`](https://pytorch.org/docs/stable/generated/torch.nn.MaxUnpool2d.html#torch.nn.MaxUnpool2d) later
- **ceil_mode** – when True, will use ceil instead of floor to compute the output shape

### Flatten

- `torch.nn.Flatten` acts differently than `torch.flatten()`
- does not flatten the first dimension, as it is assumed to be the batch dimension when used in a sequential
- [SO](https://stackoverflow.com/questions/67460123/understanding-torch-nn-flatten)

## Pooling

- (+) Reduces number of parameters in model by downsampling
- (+) Makes feature detection more robust to object orientation and scale changes
- Most common pooling operation is applying `max()` over the contents of the window/kernel
- In order to downsample, stride must be > 1
- For non-overlapping pooling windows, stride must = window/kernel size
- padding of 0s is added to input feature map so that the window has enough space to act over (does not affect the max() operation)

## Dropout

- Randomly ignoring units during training
- Acts as a regularizer and prevents overfitting
- During training:
    - for each hidden layer, for each sample, for each iteration, zero out a fraction $p$ of the nodes and their corresponding activations
- During testing:
    - use all the activations, but reduce them by a factor of $p$ to account for the missing activations during training
- "[Improving neural networks by preventing co-adaptation of feature detectors](https://arxiv.org/abs/1207.0580)" (Hinton et al. 2012)
- ”Dropout: a simple way to prevent neural networks from overfitting” (Srivastava, Nitish, et al.)
- Forces neural network to learn more robust features that are more useful with many different random subsets of other neurons
    - breaks up linked neurons that are not using their full capacity by relying on each other
- Doubles number of iterations to converge but time/epoch is reduced
- Largely replaced by batch normalization in modern CNN architectures b/c dropout works better for fully connected layers
    - Don't use dropout on convolutional layers
- ([source](https://medium.com/@amarbudhiraja/https-medium-com-amarbudhiraja-learning-less-to-learn-better-dropout-in-deep-machine-learning-74334da4bfc5), [source2](https://machinelearningmastery.com/dropout-for-regularizing-deep-neural-networks/))

## Architectures

- There are many standard CNN architectures ([overview](https://www.jeremyjordan.me/convnet-architectures/))
- modern ones: Inception, ResNet, DesnseNet
- classic/historical ones: LeNet-5, AlexNet, VGG 16