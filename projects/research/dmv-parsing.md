---
layout: page
title: DMV Parsing
categories: []
tags: []
status: publish
type: page
published: true
meta:
  _edit_last: '1'
  _wp_page_template: default
---
*Dependency Parsing With DMV*

We built a dependency parser based upon the dependency model with valence (DMV) created by Klein and Manning. We used this model to parse part-of-speech (POS) tag dependencies in the Wall Street Journal corpus without punctuation of sentences with less than or equal to ten words: WSJ10. We trained the dependency grammars using the inside outside algorithm for probabilistic context free grammars (PCFGs). To make use of this algorithm we first convert our dependency grammar into a split-head CFG before parsing, and then after parsing we convert the split-head CFG parse tree back into a dependency grammar.

<p class="center"><img alt="split tree"
src="/assets/images/split_tree_exp.png"/></p>

Python <a href="https://github.com/pld/dep2pcfg">code</a> used for this project is available.
