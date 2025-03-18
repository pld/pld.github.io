---
layout: post
title: Automated Infrastructure with Pallet and Clojure
categories:
- General
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---

At Ona we are rebuilding our data management platform. We are
starting with a light weight front-end that will serve up content pulled
from the REST API of our [current application](https://github.com/onaio/onadata/).
We are aiming to have the back-end in [Clojure](http://clojure.org), the front-end
in [ClojureScript](https://github.com/clojure/clojurescript), and the infrastructure
in Clojure using [Pallet](http://palletops.com/). We are excited to have a
single (and a great) language handle all of these responsibilities.

We are still at a very early stage but we are a distributed team and like to
have our apps on development boxes as we go. This allows us to share a common
reference point, give mini-demos, and QA each other's changes. Like [Fabric](http://www.fabfile.org/) for Python
and [Capistrano](http://capistranorb.com/) for Ruby, Pallet let's us do quick
deploys of the latest master or branch code.

Even better, Pallet let's us write Clojure to bring up new clusters, similarly to [Puppet](http://puppetlabs.com/), [Chef](http://www.getchef.com/), or [Ansible](http://ansibleworks.com/) &ndash; but in Clojure. We deploy
to EC2 on AWS and are glad to avoid spending time mucking around in the AWS GUI.
A succinct [pallet](https://github.com/onaio/ona-viewer/blob/master/pallet.clj) file
specifies the instance, the web application, and the deployment. Putting the current
code online and bringing up a server (if one doesn't already exist) is a single command:

```bash
lein do uberjar, with-profile +pallet pallet up \
--phases install,configure,deploy
```

This tells [Leiningen](http://leiningen.org/) to first create an `uberjar`,
which puts all of our app's dependencies in a single jar file. It then uses
the `pallet` profile to `install`, `configure`, and `deploy` our application. This
command is idempotent, making it easy to push the latest jar up.

A nuance we did not anticipate is that you cannot output logs to `stdout` in a
Jetty app. This is not particularly surprising, but using `stdout` was a development
configuration that we had not yet bothered to abstract.

For now we are handling this with the below [middleware wrapper](https://github.com/onaio/ona-viewer/blob/master/src/clj/ona/viewer/routes.clj#L17):

```clojure
(defn wrap-with-logger [handler verbose?]
  (if verbose?
      (logger/wrap-with-logger handler "/dev/stdout")
          (fn [request] (handler request))))
```

This does the normal logging if `verbose?` is true and otherwise does nothing.
When you run `lein ring server-headless` a handler is called which sets `verbose?`
to true. When you run the app through `java -jar ...`, as in our [pallet configuration](https://github.com/onaio/ona-viewer/blob/master/pallet.clj#L29),
`verbose?` is set to false.

The ona-viewer project is a work-in-progress and we would welcome any feedback. Check it out on [github](https://github.com/onaio/ona-viewer).
