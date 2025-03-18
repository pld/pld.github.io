---
layout: page
title: Result Diversification
categories: []
tags: []
status: publish
type: page
published: true
meta:
  _edit_last: '1'
  _wp_page_template: default
---
*Improving Result Diversity using Probabilistic Latent Semantic Analysis*

**Abstract**: IA-SELECT is a recently developed algorithm for increasing the diversity of a search result set by reordering an original document list based on manually generated clusters. In this paper we extend this approach to create a diversification framework in which arbitrary clustering methods can be used, and where the influence of clusters can be balanced against the original rank of documents. We study whether clusters that are automatically generated using probabilistic latent semantic analysis (PLSA) can compete with manually created clusters, and investigate how balancing the influence of clusters and original document rank affects diversity scores. As there are currently few datasets for evaluating diversity, we develop a new dataset, which is released with this paper. Our results show that diversification using PLSA can improve diversity, but that there is a large gap in performance between automatically and manually created clusters.

**Keywords**: result diversification, latent semantic indexing, clustering

Appears in DIR 2011, February 4, 2011, Amsterdam.  The code for the project
used Lemur for indexing and Perl for algorithms.  The paper is co-authored with
Katja Hofmann.  Download the [result
diversification](/assets/pdfs/dir2011_p_lubell-doughtie_k_hofmann.pdf) paper. The algorithms were later rewritten in Ruby and integrated into a Ruby on Rails web application.
