---
layout: post
title: "Better Bash Scripts"
date: 2014-06-25 14:13:38
categories:
---

A great Bash tip

```
I start every bash script with the following prolog:

  #!/bin/bash
  set -o nounset
  set -o errexit

This will take care of two very common errors:
- Referencing undefined variables
- Ignoring failing commands
```

Thanks [Robert](http://robertmuth.blogspot.com/2012/08/better-bash-scripting-in-15-minutes.html)
