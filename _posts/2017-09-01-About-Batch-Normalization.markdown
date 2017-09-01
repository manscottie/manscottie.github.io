---
layout: post
title:  "About Batch Normalization and Dropout"
date:   2017-09-01 14:20:00 +0800
categories: Maching Learning
---
These days I am taking the Deep Learning Specialization offered by Andrew Ng.  I learnt about batch normalization (BN) and Dropout.  Then I spend time to use them.  Following are what I feel after playing the BN and Dropout, they may be incorrect as I don't have strong math and statistic background to prove them.

The BN layer should be placed after the linear layer and before the activation layer, just like what have been told in the lecture video.

My understanding is that the use of BN layer is to speed up the learning or in other words to reduce the number of iterations used to achieve a low-enough cost. Then why BN layer can do such a job? To speed up the learning, we would like the backprop can successfully update the weight and bias, meaning that we want in every backprop the delta weight and delta bias are large enough. To achieve it, we want the activation function operates at the non-saturated part (e.g. where slope is not almost zero). BN layer is hence should be right before the activation layer to normalize the linear layer output so that the activation function is operated at the non-saturated part no matter how the linear layer output distribution is. Imagine if the linear layer output is poorly distributed such that the output of activation is at those almost-zero-slope regime, backprop will then be very inefficient, adding the BN layer after the activation layer is therefore not helping the backprop.

About the efficiency of using Dropout, my feeling is that the number of units in each hidden layer plays an important role.  For example, if the number of units in a layer is not big enough, it is very difficult to hit the right keep probability.  In other words, at least to me, I do feel dropout is a kind of technique being "quantized". For example, if a layer has 12 units, with dropout we can only have 11 effective units but not something 11.x effective units. The turning is kind of being "quantized". This contrasted to L2 Reg., where the parameter lambda can be tuned continuously.