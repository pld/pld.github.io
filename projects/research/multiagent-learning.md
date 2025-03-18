---
layout: page
title: Multi-agent Learning
categories: []
tags: []
status: publish
type: page
published: true
meta:
  _edit_last: '1'
  _wp_page_template: default
---
*Multi-agent Reinforcement Learning*

**Abstract**: We address the problem of how autonomous agents that sense and act in their environment can learn to choose optimal actions to achieve their goals. We will use the Q-learning algorithm, which learns optimal control strategies from delayed rewards, even when agents have no prior knowledge of the effects of their actions on the environment. We will experiment with two different strategies for choosing actions, an ε-greedy strategy that randomly chooses actions and an ε-greedy strategy that chooses actions weighted by their estimated value.

![joint policy](/assets/images/multiagent-learning/rand_joint.png)

The above graph, random choice, converges slower than the below graph,
probabilistic choice, which uses a Boltzmann-like  annealing.  All [project
code](https://github.com/pld/mas-q-learning) was written in Python.  Download
the [multi-agent learning](/assets/pdfs/marl_mas_2.pdf) project report.

![joint policy](/assets/images/multiagent-learning/prob_joint.png)

This was a joint project with Davide Modolo.
