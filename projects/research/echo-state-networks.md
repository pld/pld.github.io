---
layout: page
title: Echo State Networks
categories: []
tags: []
status: publish
type: page
published: true
meta:
  _edit_last: '1'
  _wp_page_template: default
---
*Using Echo State Networks to Count without a Counter*

**Abstract**: Echo state networks are a class of recurrent neural networks containing a set of nodes and recurrent connections not subject to adjustment during training and thereby greatly reducing the amount of time needed for training and the size of the solution space. Much work has been done applying this relatively new type of network to common problems in parallel distributed processing, such as past tense prediction and sentence processing. We continue this and apply echo state networks to the problem of counting without a counter. We find that echo state networks are successfully able to learn to count by predicting the length of input in a context free grammar. We find that networks with smaller reservoirs produce more general solutions, which perform better on test data.

<p class="center">
<img alt="echo state network" src="/assets/images/nn_esn.png"/>
</p>

In the above image we see the network predicted transitions in a context free
grammar.  All code was written in Matlab.  Download the [echo state
networks](/assets/pdfs/nnsr_p_lubell-doughtie.pdf) paper.
