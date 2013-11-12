---
layout: post
title:  "Quickly Customize a Heroku Buildpack"
date:   2013-11-12 13:22:58
categories: heroku devopts deployment
---

When you do things the way you're "supoosed" to in Rails, or Node, or super-mega-awesome-platform X, Heroky buildpacks, "just work".
But every so often customization is required. Here's a quick guid to customizing an existing buildpack.

In my case I wanted to run "make" after npm in the nodejs buildpack. I think there's prolly an easier way to get the same effect, but
after a while digging around online, this was the simplest thing to get the job done.

1. Find the buildpack you want to extend and fork it on github
2. clone the forked repo
3. Edit bin/build and commit and push your changes
4. Tell Heroku to use your buildpack

{% highlight bash %}
  heroku config:set BUILDPACK_URL=https://github.com/padwasabimasala/heroku-buildpack-nodejs-with-makefile-support
{% endhighlight %}
