# Magnet Loss in PyTorch

This is a direct conversion from the Tensorflow version: [pumpikano/tf-magnet-loss](https://github.com/pumpikano/tf-magnet-loss)


![Figure 3 from paper](https://raw.githubusercontent.com/pumpikano/tf-magnet-loss/master/magnet_loss.png)

"[Metric Learning with Adaptive Density Discrimination](http://arxiv.org/pdf/1511.05939v2.pdf)" introduced
a new optimization objective for distance metric learning called Magnet Loss that, unlike related losses,
operates on entire neighborhoods in the representation space and adaptively defines the similarity that is
being optimized to account for the changing representations of the training data.

## Implementation

Tested with python 3.6 + pytorch 0.4 + cuda 9.1

The Magnet Loss function is implemented in `magnet_ops.py`. The function `magnet_loss` implements the exact
loss function and requires class and cluster labels for each example. This formulation allows varying numbers
of clusters per class. The `minibatch_magnet_loss` is a thin wrapper around `magnet_loss` that assumes a
particular batch structure as described in section 3.2 of the paper. This minibatch loss, when combined with
the sampling procedure for batches described in the paper, is a stochastic approximation of the exact loss.

The module `magnet_tools.py` contains a `ClusterBatchBuilder` class that encapsulates the state and logic for
computing, maintaining, and sampling from a cluster index of the training data.

## Experiments

A simple experiment of MNIST shows that the implementation works, but isn't an interesting case for comparison
to other losses since MNIST is too simple.
