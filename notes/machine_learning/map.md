# Map of ML

## Supervised Learning

## Unsupervised Learning

### Auto-Encoders
num input layers = num output layers but smaller num hidden layers.

This forces the network to learn a compressed representation of the data. A simple autoencoder could take 100 dimensional data (100 input units) and represent it low dimensionally as 50 dimensions if using 50 hidden units.

Relies on the input data having features (completely random noise would be tough to learn anything from)

Mathematically, it can be thought of as trying to learn an approximation to the identity function so the output is similar to the input. Allows us to discover interesting structure about the data.
