---
layout: post
title:  "Up and running with multiple buildpacks"
date:   2013-11-12 13:32:58
categories: heroku devopts deployment
---

About ten minutes ago (literally) I wrote about extending buildpack behavior by forking the build pack and modifying the build script.
Depending on what you're trying to do there might be an eaiser way. In may case all I wanted was to run the 'make' command after npm install.
For that use case the multi buildpack might be a better option.

The (multi buildpack)[https://github.com/ddollar/heroku-buildpack-multi] allows you run multiple buildbacks sequentially.

## One
Add a .buildpacks file the root of your app and specifiy the buildpacks you want to use in order.

{% highlight bash %}
echo "https://github.com/timshadel/heroku-buildpack-nodejs.git
https://github.com/heroku/heroku-buildpack-c.git" > .buildpacks
{% endhighlight %}

## Two
Configure Heroku to use the multi buildpack, and it will detect the .buildpacks file and run the appropriate build packs

{% highlight bash %}
  heroku config:set BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi
{% endhighlight %}

You may have to tweak the environment a bit to get make to run right.

## Three
Set the path

{% highlight bash %}
  heroku config:set PATH=bin:node_modules/.bin:/usr/local/bin:/usr/bin:/bin
{% endhighlight %}

## Four
Enable user-env-compile in order for make to be able to find the node executable

{% highlight bash %}
  heroku labs:enable user-env-compile
{% endhighlight %}
