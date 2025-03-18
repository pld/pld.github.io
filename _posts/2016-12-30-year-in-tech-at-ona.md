---
layout: post
title: Tech at Ona&#58; What We Built in 2016
categories:
- General
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---

This is a [reposting](https://blog.ona.io/general/2016/12/30/year-in-tech-at-ona.html) or an article for the [Ona blog](https://blog.ona.io/).
It's been a big year for the Ona tech team! In this post, we look at what we built in 2016.

### Ona platform tech in 2016

In 2016 we added more new features to the Ona platform than in the previous two years combined. Here's a run-down of select features we added to Ona in 2016:

* CSV uploads &#8211; Upload any CSV into Ona and we'll automatically build an XLSForm from the CSV's columns with data types guessed based on the data. E.g. if a column has only dates we'll assume it should be formatted as a date type, but give you option to adjust that.
* Photo gallery &#8211; View only the images from your dataset in a grid-based gallery or full-screen slideshow.
* [Dynamic form linking](https://blog.ona.io/features/2016/10/27/Linking-datasets-in-Ona.html) &#8211; Use the data in one form to populate questions in another. For example, you could use a school registration form to collect the list of all the schools in your district, and then in a school performance form you could have a drop-down menu where users choose one of the schools from the registration form and then add additional performance data about that school.
* [RapidPro integration](https://blog.ona.io/features/2016/08/16/ona-to-rapidpro.html) &#8211; Forward incoming data from Ona to RapidPro and trigger flows based on that data. E.g. send out a text message to a number submitted in an Ona form with a message based on that submission's data.
* [Google Sheets integration](https://blog.ona.io/features/2016/08/02/google-sheets.html) &#8211; Connect your dataset to Google Sheets and as you submit new data, or edit existing data, Ona will update your spreadsheet. You can use this to create lightweight dashboards with realtime data collected using Ona.
* [HXL support](https://blog.ona.io/features/2016/06/22/full-HXL-support.html) &#8211; Tag your dataset columns with HXL codes for easy integration into the [Humanitarian Data Exchange](https://data.humdata.org/) and other existing datasets or repositories.
* [Save charts to a dashboard and chart group by](https://blog.ona.io/data/2016/05/05/release-notes.html) &#8211; Create charts with one column grouped by another column and save any charts you create to a dashboard.

In addition to the new features above, we improved performance to handle the 4.5 million new submission we received. This was a jump from an average about 6,500 submission a day in 2015 to 12,500 per day in 2016. Next year we'll be putting even more focus on performance and fix anything that might be slowing you down.

### OpenSRP tech in 2016

We've made significant improvements in the OpenSRP platform. As the technical lead on [OpenSRP](http://smartregister.org/) our biggest task this year was transitioning the server and client to use an [Event/Client data model](https://smartregister.atlassian.net/wiki/display/Documentation/EC+Data+Model). This helped us support more efficient client-server data synchronization.

We'll continue to be busy with OpenSRP next year. We're about to roll out a number of new implementations, including a generic vaccination register. And we’re also very excited that the UNICEF Innovation Fund invested in [OpenSRP](https://blog.ona.io/general/2016/12/06/Unicef-Innovation-Funding-OpenSRP.html) as one of their inaugural five technology investments.

### Free Open Source Software at Ona in 2016

We're still improving the documentation and doing clean up, but in late-2016 we published an updated version of our core data collection application, [onadata (Github)](https://github.com/onaio/onadata/). This fixes some serious issues encountered when running at scale, introduces a more robust permissions model based around projects, and stores all data in PostgreSQL + PostGIS database. All new development will take place in this repository on the master branch with [stable releases (Github)](https://github.com/onaio/onadata/releases) tagged.

We've continuously updated [milia (Github)](https://github.com/onaio/milia), our Clojure/Script Ona Client API library. We've added libraries to interact with more API endpoints and improved overall stability. Also in the Clojure world, we've been incrementally adding functionality to our Clojure/Script utilities library [chimera (Github)](https://github.com/onaio/chimera) and our data viewer library [hatti (Github)](https://github.com/onaio/hatti).

This year we released an [Ona to R integration](https://blog.ona.io/general/2016/04/15/Ona-R-Integration.html). This lets you load realtime datasets directly into your R scripts. [Forest Carbon](http://forestcarbon.com/) used Ona.R to write an R [Shiny](https://shiny.rstudio.com/) web application that [automated analysis and feedback](https://blog.ona.io/features/2016/07/27/ona-to-r.html). The source code for [ona.R (Github)]((https://github.com/onaio/ona.R)) is freely available, we're looking forward to your patches and extensions!.

Finally, we've released a public version of the [STEPS](https://play.google.com/store/apps/details?id=com.onaio.steps) app developed for the World Health Organization's STEPwise approach to noncommunicable disease risk factor surveillance. If you're interested check out the the code for the Android [steps-app (Github)](https://github.com/onaio/steps-app).

We're excitedly looking forward to an even bigger year in 2017. Happy new year from the Ona technology team!
