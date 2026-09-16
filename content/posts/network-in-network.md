+++
date = '2021-10-06'
draft = false
title = 'What are 1×1 Convolutions?'
tags = ['Computer Vision']
summary = 'A gentle introduction to 1×1 Convolutions'
+++

# What are 1×1 Convolutions?

I came across 1×1 convolution when reading some research papers and realized we never covered this term in my university syllabus. I quickly researched it and here's what I learned in less than 5 minutes.

## A Quick Overview of Convolutions

In mathematics, the term **convolution** refers to the mathematical operation on two functions (f and g) which produces a third function (f\*g)[1]. In Deep Learning, it is performed between the **input data** (which might be an image) and a **kernel** or **filter** (a matrix of numbers), resulting in a **feature map**.

**Key components:**

- The **input data** is a 3D array of **height × width × depth**. Where depth is the number of channels: 1 for grayscale images and 3 for RGB images.
- A **filter/kernel** is a 3D array of weights with **height × width × channels**. Most kernels are **symmetrical**, so height and width are the same. The number of channels in the kernel must match the depth of the input image[2].
<figure>
{{< image src="/images/network-in-network/cross-correlation-computation.png" alt="Cross-correlation computation with 2 input channels" position="center" >}}
<figcaption>Cross-correlation computation with 2 input channels [2]</figcaption>
</figure>

**Why symmetric kernels?** What happens if the kernel size is bigger than the input? These questions deserve their own articles. For now, let's cover the last two essential concepts:

- **Stride:** The number of pixels we move during each step in a convolution. Default value is one.
- **Padding:** The number of pixels added to an image's outer layer. These extra pixels are filled with zeros.

<figure>
{{< image src="/images/network-in-network/stride-padding.gif" alt="Stride and padding visualization" position="center" >}}
<figcaption>Figure 2: Stride and padding = 1 [3]</figcaption>
</figure>

We can see that the output is smaller than the input data. Use the formula below to calculate the output dimension:

<figure>
{{< image src="/images/network-in-network/convolution-output-formula.png" alt="Convolution Output Formula" position="center" >}}
<figcaption>Figure 2: Convolution Output Formula [3]</figcaption>
</figure>

## 1×1 Convolutions

Typically we use 3\*3 or 5\*5 kernels, which would result in a single feature map. One filter can be used to detect one type of spatial feature in the image (eg: vertical edge), in order to capture multiple features we use multiple filters of the same size. The result is a feature map with multiple channels.

<figure>
{{< image src="/images/network-in-network/rgb-image.png" alt="RGB image convolved with two 3x3x3 filters" position="center" >}}
<figcaption>Figure 3: RGB image convolved with two 3×3×3 filters [4]</figcaption>
</figure>

Similarly, 1\*1 Convolution is applying 1\*1 kernel with stride 1 and 0 paddings. The result of this is a scaled version of the input data which has the same height and width with a single channel in the case of a single filter. We do this by taking element-wise multiplication and adding across all the channels as we do for every other convolution.

<figure>
{{< image src="/images/network-in-network/64_64_192.png" alt="64x64x192 Input image with 1x1 kernel with 192 channels" position="center" >}}
<figcaption>Figure 4: 64×64×192 Input image with 1×1 kernel with 192 channels [5]</figcaption>
</figure>

## Why Should We Care?

- **Non-Linearity** : The output feature map can be passed through a non-linear activation function (like ReLU) to introduce non-linearity while maintaining the input's height and width. Other kernel sizes may result in different dimensions.

- **Downsampling Channels** : As the network gets deeper we end with a lot of feature maps and the network gets complex. Like we use \*_pooling layers_ to downsample the _dimensions_, we can use 1\*1 convolutions to downsample the _number of channels_ by choosing the desired number of 1\*1 Conv filters.

<figure>
{{< image src="/images/network-in-network/downsampling.png" alt="Downsampling channels with 1x1 Conv" position="center" >}}
<figcaption>Figure 5: Downsampling channels with 1×1 Conv [6]</figcaption>
</figure>

- **Reducing computation cost** : This technique can be used to reduce the computational cost. Applying filters like 3\*3 to a large number of channels like 192 is expensive instead, we can reduce the number of channels using 1\*1 Conv before applying typical filters to reduce the cost.

<figure>
{{< image src="/images/network-in-network/before.png" alt="Computation cost before using 1x1 Conv" position="center" >}}
<figcaption>Figure 6a: Before using 1×1 Conv - Large computational overhead</figcaption>
</figure>

<figure>
{{< image src="/images/network-in-network/after.png" alt="Computation cost after using 1x1 Conv" position="center" >}}
<figcaption>Figure 6b: After using 1×1 Conv - Significantly reduced computation [7]</figcaption>
</figure>
---

This gives you a brief introduction to 1×1 convolutions. For more details, check out the original paper **"Network in Network"** by Min Lin, et al.

## References

[1] "Convolution — Wikipedia", En.wikipedia.org, 2021. [Online]. Available: https://en.wikipedia.org/wiki/Convolution.

[2] "6.4. Multiple Input and Multiple Output Channels — Dive into Deep Learning 0.17.0 documentation", D2l.ai, 2021. [Online]. Available: https://d2l.ai/chapter_convolutional-neural-networks/channels.html.

[3] V. Tony, "Pytorch [Basics] — Intro to CNN", Tony Ma, 2021. [Online]. Available: https://tonymazn.wordpress.com/2021/02/22/pytorch-basics-intro-to-cnn/.

[4] M. Deshpande, "Convolutional Neural Network — II", Medium, 2021. [Online]. Available: https://towardsdatascience.com/convolutional-neural-network-ii-a11303f807dc.

[5] K. Bai, "A Comprehensive Introduction to Different Types of Convolutions in Deep Learning", Medium, 2021. [Online]. Available: https://towardsdatascience.com/a-comprehensive-introduction-to-different-types-of-convolutions-in-deep-learning-669281e58215.

[6] A. Johnson, "Fundamental Terms in Computer Vision", Medium, 2021. [Online]. Available: https://blog.goodaudience.com/fundamental-terms-in-computer-vision-d68dfb1c7d.

[7] R. Sakthi, "Talented Mr. 1X1: Comprehensive look at 1X1 Convolution in Deep Learning", Medium, 2021. [Online]. Available: https://medium.com/analytics-vidhya/talented-mr-1x1-comprehensive-look-at-1x1-convolution-in-deep-learning-f6b355825578.
