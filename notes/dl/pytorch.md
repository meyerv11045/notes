# PyTorch Blitz

autograd- calculates and stores the gradients for each model param in each parameter's `.grad` attribute

simple training loop:

``` python
import torch

model = torchvision.models.resnet18(pretrained=True)
data = torch.rand(1,3,64,64) # 64 x 64 img with 3 channels
labels = torch.rand(1,1000)

prediction = model(data) # Forward pass

loss = (prediction - labels).sum()

loss.backward() # backward pass (backprop)

# register all the model params in the optimizer
optimizer = torch.optim.SGD(model.parameters(),lr=1e-2,momentum=0.9)
optimizer.step() # initiate gradient descent
```

if a parameter in a NN does not `requires_grad` then these params are known as frozen meaning the gradients won't be recomputed. NOTE: `torch.no_grad` also does same thing ([read more](https://pytorch.org/docs/stable/generated/torch.no_grad.html)). also useful for finetuning pretrained networks where you only want to modify the params in the classifer layers to make predictions on the new labels:

``` python
model = torchvision.models.resnet18(pretrained=True)

# Freeze all the parameters in the network
for param in model.parameters():
    param.requires_grad = False

# replace last linear layer (the classifier) with new unfrozen classification layer  
model.fc = nn.Linear(512, 10)

```

## torch.nn pkg

`nn.Module` contains layers and a `forward(input)` method that returns the output. Can build modules of networks that can be used in other networks. Only have to define the forward function and the backward function will be automatically defined using autograd (relies on autograd parsing the operations in the forward function and creating the appropriate computational graph of all the derivatives)

`net.parameters()` returns the learnable parameters of a nn module

only supports mini-batch inputs, no single input samples

``` python
import torch.nn as nn
import torch.nn.functional as F

class Net(nn.Module):
    def __init__(self):
        super().__init__()
        self.conv1 = nn.Conv2d(3, 6, 5)
        self.pool = nn.MaxPool2d(2, 2)
        self.conv2 = nn.Conv2d(6, 16, 5)
        self.fc1 = nn.Linear(16 * 5 * 5, 120)
        self.fc2 = nn.Linear(120, 84)
        self.fc3 = nn.Linear(84, 10)

    def forward(self, x):
        x = self.pool(F.relu(self.conv1(x)))
        x = self.pool(F.relu(self.conv2(x)))
        x = torch.flatten(x, 1) # flatten all dimensions except batch
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.fc3(x)
        return x

net = Net()
```

A loss function takes the (output, target) pair of inputs, and computes a value that estimates how far away the output is from the target. Many are provided by the nn pkg such as `nn.MSELoss` but you can also define your own 

In order to backpropagate the error/loss, we need to clear the existing gradients (`net.zero_grad()`) and then call `loss.backwards()`

https://pytorch.org/docs/stable/nn.html

updating the weights can be done using the below code since `weights = weights - learning rate * gradient` for SGD: 

``` python
learning_rate = 0.01
for f in net.parameters():
    f.data.sub_(f.grad.data * learning_rate)
```

using the torch.optim module lets you easily use other update rules like SGD, Adam, RMSProp, etc. 

``` python
import torch.optim as optim

# create your optimizer
optimizer = optim.SGD(net.parameters(), lr=0.01)

# in your training loop:
optimizer.zero_grad()   # zero the gradient buffers
output = net(input)
loss = criterion(output, target)
loss.backward()
optimizer.step()    # Does the update
```

## recap

- `torch.Tensor` - A *multi-dimensional array* with support for autograd operations like `backward()`. Also *holds the gradient*w.r.t. the tensor.
- `nn.Module` - Neural network module. *Convenient way of encapsulating parameters*, with helpers for moving them to GPU, exporting, loading, etc.
- `nn.Parameter` - A kind of Tensor, that is *automatically registered as a parameter when assigned as an attribute to a* `Module`.
- `autograd.Function` - Implements *forward and backward definitions of an autograd operation*. Every `Tensor` operation creates at least a single `Function` node that connects to functions that created a `Tensor` and *encodes its history*.





## gradient clipping 

``` python
optimizer.zero_grad()
loss.backward()

# by value
torch.nn.utils.clip_grad_value_(model.parameters(), clip_value=1)

# by norm
# torch.nn.utils.clip_grad_norm_(model.parameters(), clip_norm=1)

optimizer.step()
```

- Note that it stacks all the paremeters into a single vector then performs the clipping 
    - we want to just clip the gradients from th



## hooks

- tensor.backward() starts the backward pass on the computational graph with a default starting gradient value of 1.0
- allow us to inspect (and possibly change) gradients as they flow backwards through the graph 
- hooks get called on tensors in the order they were added
- `.retain_grad()` stores the grad on non-leaf/intermediate nodes in the computational graph
- when adding hooks to a intermediate node in the forward graph (stored in the backward_hooks dict), the function will also be added as a pre-hook to the corresponding node in the backwards graph to be run on the gradient before the node does its thing



``` python
def fn(grad):
  print(grad)
  return grad + 2 # if you return nothing, the same gradient as before will be used

c.register_hook(fn)
```







## loss functions

- Cross Entropy Loss- multiclass classification
    - when used for binary classification it expects 2 output features (e.g. [-2.34, 3.61])
    - Can get probability of each class by using softmax 
        - does not give meaningful probabilities in case of binary classification (will always be something like [0.3%, 99.7%])
- Binary Cross Entropy Loss- binary classification
    - expects 1 output feature (e.g. [-2.34])
    - Can easily get probability of class 1 using sigmoid on the network's output logits





- [PyTorch Training Step Dissection](https://charlesfrye.github.io/external/2021/08/24/trace-report.html)
