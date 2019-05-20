# GAN-李宏毅

## Introduction

### Basic Idea of GAN

Algorithm

![](Pic/Screenshot from 2019-05-20 11-13-15.png)

![](Pic/Screenshot from 2019-05-20 11-18-14.png)

![](Pic/Screenshot from 2019-05-20 11-20-28.png)

训练D和G的时候迭代次数各自是个hyperprameter

### GAN as structured learning

#### Why structured learning challenging

1.  One-shot/Zero-shot Learning:
   1. in classification, each class has some examples
   2. In sturcured learning,
      1. Consider each possible output as a "class"
      2. Since the output space is huge, most "classes" do not have any training data
      3. Machine has to create new stuff during testing
2. Machine has to learn to do planning
   1. Machine generates objects component-by-component, but it should have a big picture in its mind.
   2. Because the output componets have dependecy, they should be condisdered globally.

### Can generator learn by itself?

Auto-Encoder

Variational Auto-Encoder

![](Pic/Screenshot from 2019-05-20 13-22-36.png)

但这种方式中元素之间的关系容易被忽略，比如像素间位置关系。需要增加网络参数。

往往在网络结构相同的情况下，有Discriminator的GAN效果要比Auto-Encoder的Decoder更好。

### Can Discriminator generate

Discriminator: Evaluation Function, Potential Function, Energy Function

首先，Discriminator分辨像素间关系要比Generator容易得多

![](Pic/Screenshot from 2019-05-20 13-40-44.png)

如何训练Discriminator问题：

先假设Discriminator确实能够生成图片。 

​	数据库中只有正例，需要额外生成反例。

![](Pic/Screenshot from 2019-05-20 13-44-59.png)

![](Pic/Screenshot from 2019-05-20 13-57-27.png)

 

## Conditional GAN

Text-to-Image

Traditional Supervised approach: 容易产生数据集中多张Image平均的模糊图片

GAN：
	如果Discriminator只有图片的输入，那么Generator就会直接产生数据集中的图片，无视条件输入。所以Discriminator需要三种输入。

![](Pic/Screenshot from 2019-05-20 14-35-40.png)

![](Pic/Screenshot from 2019-05-20 14-38-00.png)

![](Pic/Screenshot from 2019-05-20 14-42-03.png)

上图是两种Discriminator网络结构设计，下面的结构可以将两种Negative Sample的情况分开。

### StackGAN![](Pic/Screenshot from 2019-05-20 14-50-15.png)

### ### Image-to-Image

PatchGAN

### Speech Enhancement

### Video Generation

## Unsupervised Conditional Generation

1. Direct Transfomation(For texture or color change)

   1. 直接用GAN转换，忽略Generator偷懒的问题
   2. DTN
   3. CycleGAN（CycleGAN: a Master of steganography)
      1. 容易产生hidden information，难以被发现。Cycle Consistency不一定work
      2. Dual GAN
      3. Disco GAN
   4. StarGAN(Cross-domain transformation)
      1. 其实还是用了Cycle Consistency扩展到了多个Domain

2. Projection to Common Space(Larger Change)

   ![](Pic/Screenshot from 2019-05-20 15-34-27.png)

   Training

   ![](Pic/Screenshot from 2019-05-20 15-44-02.png)

   训练中会遇到问题，因为两者分开训练，那么中间曾的codes不能通用。

   ​	a.参数共用 Couple GAN/ UNIT	![](Pic/Screenshot from 2019-05-20 15-46-04.png)

   ​	b.Domain Discriminator判断中间层embedding vector是来自与哪个Domain， 那么他就限制了这个vector中feature的distribution在两个domain中相同。

   ​	c.Cycle Consistency--Combo GAN

   ![](Pic/Screenshot from 2019-05-20 15-53-34.png)

   ​	b.Semantic Consistency--DTN，XGAN：与Cycle Consistency相似，比较latent space中embedding vector的相似程度

   ![](Pic/Screenshot from 2019-05-20 15-54-07.png)

