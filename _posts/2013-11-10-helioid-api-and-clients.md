---
layout: post
title: Ruby and Clojure client libraries for the Helioid API
categories:
- General
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---

We recently released a Helioid API that returns categorized search results.
To retrieve JSON results for a
query like "[data
analytics](http://www.helioid.com/searches/q/data+analytics)" simple append
"`?format=json`" to the URL, i.e.

[http://www.helioid.com/searches/q/data+analytics?format=json]
(http://www.helioid.com/searches/q/data+analytics?format=json)

To make this easier to use we have released open source
[Ruby](https://github.com/helioid/heliapi-rb) and
[Clojure](https://github.com/helioid/heliapi-clj) client libraries.
Install the Ruby library with:

```sh
gem install heliapi
```

then load and fetch categories using:

```ruby
require 'heliapi'

results = Heliapi.new.web('ruby apis')

results['categories'].keys
```

which returns:

```ruby
=> ['Developer',
    'Access',
    'Provides',
    'Rails',
    'Building',
    'Install',
    'Google Api Ruby',
    'Ruby Client'
]
```

To install the Clojure library add `heliapi` to your Leiningen `project.clj`
file:

```clojure
[heliapi "0.0.1"]
```

then load and fetch categories with:

```clojure
(:require [heliapi.core :as helioid])

(map #(:name %)
     (:categories (helioid/web "helioid")))
```

which returns the results as:

```clojure
=> ("search refinement"
    "search engine"
    "results"
    "helioid choroiditis"
    "intranuclear helioid inclusions"
    "intranuclear helioid"
    "new"
    "helioid search")
```

We will add features to the API and client libraries as requested.  We will
also make libraries for other languages as requested.
