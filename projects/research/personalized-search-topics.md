---
layout: page
title: Personalized Search Topics
categories: []
tags: []
status: publish
type: page
published: true
meta:
  _edit_last: '1'
  _wp_page_template: default
---
*Applying Diversity and Novelty to Personalized Search*

**Abstract**: Recent research into retrieving and reordering search results so that they cover a maximum number of topics and information needs has gained traction as a means to assist navigation through the explosion of available online information. This problem is also addressed by personalized search: the retrieving and reordering of search results biased to the preferences of a particular user. We investigate a search personalization system that builds a user model from the latent topics mined from their queries and clicked documents. We find that a user’s clicked documents exist in a specific area of the latent topic space. By “diversifying” search results biased to our user model we can reorder search results to the user’s preferences.

<p class="center"><img alt="personalized topic space"
src="/assets/images/ls_personalized.png"/></p>

Above is a scatter plot of the location of each query and document the user
clicked on for that query in topic space. We see that the user appears to occupy a distinguished manifold in 3-topic space.

All code written in R and Ruby.  Download the [personalize search
topics](/assets/pdfs/ls_project_p_lubell-doughtie.pdf) paper.
