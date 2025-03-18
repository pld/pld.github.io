---
layout: page
title: Photocracy
categories: []
tags: []
status: publish
type: page
published: true
meta:
  _edit_last: '1'
  _wp_page_template: default
---
The Photocracy web application was written in <em>Ruby on Rails</em> (2.3.x)
    using <em>HAML</em> and <em>SASS</em> for templating and <em>JQuery</em>
    for JavaScript.  It was a multilingual site (Chinese, English, Japanese,
            and Spanish) and relied on geolocation to guess and set the
    language.  Photo uploads where handled by the <em>attachment\_fu</em> plug-in and integrated with the Flickr API.  Photo pairs were requested and loaded from the Pairwise API using <em>XML</em>.  The application recorded comprehensive tracking statics of all user movement.  Back-end analysis used the <em>spawn</em> plug-in to create charts of these tracking statistics with the <em>gnu_plotter </em>plug-in.

Below is a screen shot of the original photocracy front page.  The  front page had an animated progress bar (shown in unfilled  grey, which would become blue) and kept track of cached prompts so the  user would not experience any latency between votes.

<p class="center">
<a href="/assets/images/photocracy/photocracy_front_screen1.png"><img
title="photocracy_front_screen"
src="/assets/images/photocracy/photocracy_front_screen1.png" alt="Photocracy
Front Screenshot" width="600" /></a></p>

Project Description: Photocracy is a research project to develop a new form of social data collection that combines the best features of quantitative and qualitative methods. Using the power of the web, we are creating a data collection tool that has the scale, speed, and quantification of a survey while still allowing for new information to "bubble up" from respondents as happens in interviews, participant observation, and focus groups.

<p class="center">
<a href="/assets/images/photocracy/photocracy_list_screen.png"><img
title="photocracy_list_screen"
src="/assets/images/photocracy/photocracy_list_screen.png" alt="Photocracy List
Screenshot" width="600" /></a></p>

Above is a screen shot of the photo listing page.  The source code for my version of Pairwise is <a href="https://github.com/pld/photocracy">here</a>.   The Photocracy project has changed and now has a new developer, it is available <a href="http://www.photocracy.org/">here</a>.
