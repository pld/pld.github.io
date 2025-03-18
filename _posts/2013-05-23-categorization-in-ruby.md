---
layout: post
title: Categorizing Text in Ruby
categories:
- General
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
We have open sourced the [categorization
libary](https://github.com/helioid/categorize) that powers the fast dynamic
labels and clusters on the [Helioid](http://www.helioid.com) site.  This
library is built to prioritize performance over accuracy.  The library takes
label quality into account by first generating a set of labels and then assigning
documents to those labels, we have found that this increases the likelihood of producing
meaningful labels.

The below example shows how to create a set of labeled cluster from documents. First
include the categorize library.

```ruby
require 'categorize'

include Categorize
```

Then define your set of documents.

```ruby
documents = [
  'lorem ipsum dolor',
  'sed perspiciatis unde',
  'vero eos accusamus',
  'vero eos accusamus iusto odio'
]
```

Now make a model based on an additional query term, `lorem`, in this case.

```ruby
Model.make_model('lorem', documents)
=> {
   'ipsum'            => [0],
   'sed perspiciatis' => [1],
   'vero'             => [2, 3]
}
```

The model output is a map of cluster labels to documents within those clusters.
Install the gem and [try it out](https://github.com/helioid/categorize).
