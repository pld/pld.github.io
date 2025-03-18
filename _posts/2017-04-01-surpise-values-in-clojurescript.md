---
layout: post
title: Calculating Surprise Values in ClojureScript
categories:
- General
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---

Earlier this year I rewrote Ben Birnbaum's [outlier-detect](https://github.com/benb111/outlier-detect) Python code in ClojureScript and combined it with some very simple [React](https://facebook.github.io/react/) glue code to build an on-demand [s-Value calculator](https://github.com/pld/calculon). s-Values represent the amount of surprise in a grouped value relative to other data in a larger dataset. A higher s-Value means the data is less expected.

The output is based on what Birnbaum presented as a screenshot of a prototype in his dissertation, [Algorithmic approaches to detecting interviewer fabrication in surveys](http://bbirnbaum.com/assets/publications/dissertation.pdf). In that version the color of the text changed depending on the s-Value. In my version the text color is constant but the background color of the cells are different shades of red, with darker shades indicating an s-Value more standard deviations from the mean for that row.

<img alt="ghetto" src="/assets/images/s-values.png" width="600px"/>

You can use the [web interface](http://peet.ldee.org/calculon/) to generate s-Values by URL from a JSON file represented as a list of maps, or use your [Ona.io](https://ona.io) credentials to load data in your account. This is very much a work in progress, please get in touch or open an [issue](https://github.com/pld/calculon/issues) with any feedback or ideas you have.
