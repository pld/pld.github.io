---
layout: page
title: Pairwise API
categories: []
tags: []
status: publish
type: page
published: true
meta:
  _edit_last: '1'
  _wp_page_template: default
---
Pairwise was a <em>Ruby on Rails</em> (2.3.x) web application that accepted a data set of users, questions, and items then created pairs of items for users and questions and returned these through an <em>XML </em>API.  Clients could send back responses as a vote on one pair in the set.  Based on these votes Pairwise performed data analysis to determine the ranking of items for each question.  Additionally, singular value decomposition (<em>SVD) </em>was performed on the items and vote data to find sets similar items.

The source code for my version of Pairwise is <a
href="https://github.com/pld/pairwise">here</a>. I have also written a [Ruby on
Rails plugin](https://github.com/pld/ror-pairwise) for
interactive with a Pairwise API.  Work on
the [Pairwise API](https://github.com/allourideas/pairwise-api) has been continued by a new developer.
Below is a digram of the role the pairwise API plays.  

<p class="center"><img title="pairwise diagram"
src="/assets/images/photocracy/pairwise_diagram.png" alt="Pairwise Front
Screenshot" width="400" /></a></p>

With the Pairwise Web Service anyone can build community-generated and community-sorted websites. These websites let the best ideas in your group or organization "bubble to the top" all in a democratic, transparent, and bottom-up process.

For example, the <a href="http://www.dailyprincetonian.com/2009/01/12/22505/">Princeton Undergraduate Student Government</a> used a site like this to learn about the best ways to  improve campus  life. In a matter of weeks, more than 2,000 students  contributed more  than 40,000 votes on more than 300 suggestions, about  100 of which were  uploaded by the students themselves.

In addition to text, community-generated and  community-sorted  information websites can be used for to handle images as was done in <a href="http://www.photocracy.org/">Photocracy</a>, a project to study national identity and cross-national perceptions.
