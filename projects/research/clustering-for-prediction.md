---
layout: page
title: Clustering for Prediction
categories: []
tags: []
status: publish
type: page
published: true
meta:
  _edit_last: '1'
  _wp_page_template: default
---
*Supervised and Unsupervised Clustering for Instance Response Variable
Prediction*

**Abstract**: We present an incremental approach to cluster assignment which predicts the response variables for a set of instances based upon those assigned to instances that are near it in latent topic space. The method uses a novel combination of supervised clustering and unsuper- vised clustering to reduce the number of labeled instances needed for accurate classification. In experiments on the political blog corpus we find that predicting response variables based on unsupervised clustering and supervised labeling of a limited number of instances results in per- formance competitive with that produced by supervised labeling for all instances.

![cluster_response_prediction](/assets/images/cluster_response_prediction.png)

The above plot shows the training size versus error, we see that, generally, the clustered method is only able to outperform the supervised baseline (Predicted) when there are a larger number of training instances.

All code for this project was written in R and used the LDA package.  Download
the full [cluster for prediction](/assets/pdfs/mlpm_p_lubell-doughtie.pdf) paper.
