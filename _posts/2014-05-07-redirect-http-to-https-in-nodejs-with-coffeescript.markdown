---
layout: post
title: "Redirect Http to Https in Nodejs with CoffeeScript"
date: 2014-05-07 09:01:15
categories:
---

How to redirect http to https in NodeJS with CoffeeScript

```coffeescript
app.configure 'production', () ->
  app.use (req, res, next) ->
    schema = (req.headers['x-forwarded-proto'] || '').toLowerCase()
    if (schema == 'https')
      next()
    else
      console.log 'redirecting to https'
      res.redirect 'https://' + req.headers.host + req.url
```

credit https://gist.github.com/youtalk/3216781
