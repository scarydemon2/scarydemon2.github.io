---
layout: default
title: Aspect-based sentiment analysis method based on text style transfer
description: The patent is a by-product of LEGO-ABSA's research
---

![Link](figure/patent1.jpg)

## Motivation

Generative methods often have large errors in generating sentiment polarity. For example, multiple sentiment polarities may coexist in the same sentence. In the model's generated result, the expression of a stronger emotion will mislead the classification results of other emotions.

For instance, in the comment "The sound quality of the speaker is very good, highly recommended, and the included mouse has five sensitivity levels to choose from," both positive and neutral sentiments are present, but the model is likely to classify the sentiment polarity of the mouse's sensitivity as positive.

There are multiple reasons for this phenomenon, including redundant and potentially implicit sentiment in the original input expression.

## Method
<!-- 
如果使用生成式模型解决ABSA问题，那么这个任务可以简单建模为input-->generative model-->output。 output中的信息熵是包含答案的最低的信息熵，而input中的信息熵却是最多的。正是由于这些多出来的额外的熵，导致误差的产生。因此如果我们能够将这个任务换成input-->generative model-->input'-->output,其中input'为风格转换后的input，其信息熵介于input和output之间，通过这种方法可以避免情感极性误差(类似于当你进行细粒度信息抽取时，如果先进行摘要然后再进行抽取，那么任务难度会降低)。 -->
If a generative model is used to solve the ABSA problem, the task can be simply modeled as *input->generative model->output*. The information entropy in the output contains the lowest entropy that includes the answer, while the input has the most entropy. It is precisely because of these extra entropies that errors occur. Therefore, if we can transform this task into *input->generative model->input'->output*, where input' is the input after style transfer and its entropy is between the input and output, we can avoid sentiment polarity errors (similar to when performing fine-grained information extraction, if we first summarize and then extract, the task would become easier).

专利包含3个阶段

第一阶段：我们使用ABSA数据集的output-->generative model-->input。这种操作十分反直觉，output中的熵永远比input低，所以理论上generative model不可能完美得补全input，但是model仍然能够尽力还原input。总之通过训练，我们得到了$model_1$

第二阶段：推理时output是不可见的，因为在推理的目标是output。那么对于input为了得到input'我们可以同样使用一个generative model进行训练。即input-->generative model 2-->$model_1(output)$,  generative model 2的作用就是将高熵input蒸馏为低熵的input'，我们称这个模型为$model_2$

第三阶段：我们在训练时直接使用



[back](./)
