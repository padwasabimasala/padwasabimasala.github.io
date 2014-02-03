---
layout: post
title: "How to Setup CircleCI to Push to Heroku"
date: 2014-01-06 10:38:29
categories:
---

Go to https://circleci.com/add-projects and follow the project

This should tigger your first build

Before you can configure CircleCI to deploy to Heroku you must Setup an API key on Heroku

https://devcenter.heroku.com/articles/authentication

Then in Circle CI

1. Add that API key to CircleCI
2. Associate a Heroku SSH key with your account

https://circleci.com/docs/continuous-deployment-with-heroku

After that edit (or create) the circle.yml file and add deployment instructions
