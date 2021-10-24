### Why CNN For Image?

#### Some pattern are much smaller than the whole image

每一个神经元不需要看整张图就就可以决定这张图有某些特性，它只连接到了的一部分的区域。

#### The Same pattern appear in different regions

这些特性可能会出现在整张图的不同部分，而他们表达的含义是接近的。

#### Subsampling the pixels will not change the object

这一层在做模糊化处理，减轻训练负担，在AlphaGo里没有这一层，因为没有意义。

### The process of CNN for Image Identification

#### Convolution

先定出Filter的大小和数量，这样就可以通过这些Filter去找出某些pattern。

Filter会和图片上的每个和它相同大小的子区域做inner product。

当某一个区域和有一个Filter算出来的很大的话，这个Filter就相当于被activate。

#### Max Pooling

For each small area in the result of convolution, we pick the max value.
The common shape of the small area is [2, 2].

#### Fully Connected Neuron Network

最后把图片摊平，丢到全连接的网络中去。

#### Colorful Image

If the image have 3 channel, the filter will have the third dimension with length 3.

In other words, the filter should take image channel into account.

### Alphago Architecture

The first hidden layer zero pads the input into [23, 23] image.

Then convolves 192 filters of shape [5, 5]. 

Each of the subsequent hidden layers from 2 to 12 zero pads the input into [21, 21] image.

Then convolves 192 filters of shape [3, 3].

Then final layer adds a different bias for each position and applies a softmax function.
