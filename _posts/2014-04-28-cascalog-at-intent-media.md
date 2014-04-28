---
layout: post
title: Cascalog at Intent Media
categories:
- General
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---

While I was at [Intent Media](http://www.intentmedia.com/) I led the data
engineering team in rebuilding and extending the Intent Media data platform. To structure and
simplify queries we relied on [Cascalog](http://cascalog.org/), a Clojure
DSL built on top of the [Cascading](http://www.cascading.org/) library that is
built on top of [Apache Hadoop](https://hadoop.apache.org/).

Cascalog is inspired by [Datalog](http://docs.racket-lang.org/datalog/) and
uses [logic programming](https://en.wikipedia.org/wiki/Logic_programming)
to simplify query expression. It is similar to
[Datomic](http://www.datomic.com/) for Clojure and the recent
[DataScript](https://github.com/tonsky/datascript) for ClojureScript. This
allows simple and concise queries, e.g. to compute the average age per country:

```clojure
(?<- (stdout) [?country ?avg] 
   (location ?person ?country _ _) (age ?person ?age)
   (c/count ?count) (c/sum ?age :> ?sum)
   (div ?sum ?count :> ?avg))
```

Jon Sondag, a data scientist at Intent Media, recently gave a presentation at
the [NYC Clojure Meetup](http://www.meetup.com/Clojure-NYC/) about Cascalog in production. His slides are embedded
below.

<script async class="speakerdeck-embed" data-id="1d217290a6cb0131c0d042bc169ecec2" data-ratio="1.2994923857868" src="//speakerdeck.com/assets/embed.js"></script>

It is great to see Cascalog being used in production data platforms.
