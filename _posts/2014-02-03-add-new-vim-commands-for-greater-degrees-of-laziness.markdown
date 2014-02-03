---
layout: post
title: "Add New Vim Commands for Greater Degrees of Laziness"
date: 2014-02-03 11:58:45
categories:
---

I got tired of typing ":new $MYVIMRC" and ":so $MYVIMRC" to edit and reload my
vim config. So I decidd to find a way to make it a bit easier. I already have
the bash aliases "rcedit" and "rcreload", so I decided to add them to vim like
so.

```
" My .vimrc

command! RcEdit :new $MYVIMRC
command! RcReload :so $MYVIMRC
```

This defines two new commands that can be called from command mode. Some might
prefer to map these to commands using a leader key, or even a function key, but
prefer them to be commands because that is how I am used to calling their more
verbose alternatives.

Here's a few things to consider.

When defining new commands they must begin with a Capital letter. The following
would be invalid

```
command! rcEdit :new $MYVIMRC
```

If you don't use bang "!" when defining a command then vim will give you an
error if the command already exists.

For example if the command were defined like this:

```
command RcEdit :new $MYVIMRC
command RcReload :so $MYVIMRC
```

Then every time the config was reloaded vim would encounter the already defined
command and issue an error like "Command already exists: add ! to replace it."

### References

* http://superuser.com/questions/376213/in-vi-how-do-i-map-t-equal-to-tabnew
* http://stackoverflow.com/questions/7114744/function-to-source-vimrc-and-gvimrc
