### Why CNN For Image

#### Some pattern are much smaller than the whole image

每一个神经元不需要看整张图就就可以决定这张图有某些特性，它只连接到了的一部分的区域。

#### The Same pattern appear in different regions

这些特性可能会出现在整张图的不同部分，而他们表达的含义是接近的。

#### Subsampling the pixels will not change the object

这一层在做模糊化处理，减轻训练负担，在AlphaGo里没有这一层，因为没有意义。

### CNN影像识别

#### Convolution

先定出Filter的大小和数量，这样就可以通过这些Filter去找出某些pattern。

#### Max Pooling

然后做模糊化处理，将几个像素点合并。如果还是很大，可以继续Convolution。

#### Fully Connected Neuron Network

最后把图片摊平，丢到全连接的网络中去。

