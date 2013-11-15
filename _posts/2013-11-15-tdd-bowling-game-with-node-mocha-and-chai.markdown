---
layout: post
title: "TDD Bowling Game with Node, Mocha, and Chai"
date: 2013-11-15 11:10:16
categories:
---

In order to better understand testing in Node I decided to work out the [Bowling Game kata](http://butunclebob.com/ArticleS.UncleBob.TheBowlingGameKata) from scratch. The kata is
an exercize to pratice the disciplines of good [TDD](http://en.wikipedia.org/wiki/Test-driven_development). But is also a good starting point for learning a new environment.

The first step was to figure out how testing was done in [NodeJS](http://nodejs.org/). After googling around I found a [good starting point by Matthew Palmer](http://palmer.im/2013/03/introduction-to-test-driven-development-with-node-js-expect-mocha/). This example uses [Mocha](http://visionmedia.github.io/mocha/) and [Expect.js](https://github.com/LearnBoost/expect.js/).

The next step was to figure out how to get a project initialized with Node. More searching revelaed that I could just use

{% highlight bash %}
  node init <my project>
{% endhighlight %}

but I wouldn't do it that way again. All I got was some annoying prompts that generated a package.json. Next time I would just generate this file by hand.

After doing some more reading about how mocha works, and with some experience using [Chai](http://chaijs.com/) the previous day, I decided to use Chai instead of Expect.js.

My final package.json looks like this.

{% highlight json %}
{
  "name": "bowling-game-js",
  "version": "0.0.0",
  "description": "Bowling Game Kata in JS with Node",
  "main": "index.js",
  "scripts": {
    "test": "mocha test"
  },
  "author": "Matthew Thorley",
  "license": "BSD"
  ,"devDependencies": {
    "mocha": "*",
    "chai": "*"
  }

}
{% endhighlight %}

Note that in addition to adding the devDependencies for Mocha, and Chai, I also added the test command "mocha test" to scripts:test.

With that in place I could write my first test. I read some of the [Mocha best practices](http://visionmedia.github.io/mocha/#best-practices) and looked at a few example projects to see how things should be setup.
Then I created a test directory, and my first test, test/bowling_game.js. In other testing frameworks I've used in tht past test files usually were named
test_something or something_test. But the common practice in this ecosystem seems favor omitting the word 'test' from filenames.

{% highlight bash %}
  mkdir test
  vim test/bowling_game.js
{% endhighlight %}

Here's my first test.

{% highlight javascript %}
var chai = require('chai')
chai.should()

var BowlingGame = require ('../bowling_game').BowlingGame

describe('new BowlingGame()', function() {
  it('should create a new BolwingGame', function() {
    game = new BowlingGame
    game.should.be.a('Object')
  })
})
{% endhighlight %}

This test fails because there is no bowling_game file or BowlingGame object. Getting it to pass is easy to do. Just add a bowling_game.js file to the root
of the project and export a BowlingGame object in it.

{% highlight bash %}
  vim bowling_game.js
{% endhighlight %}

Content of bowling_game.js

{% highlight javascript %}
exports.BowlingGame = function() {
}
{% endhighlight %}

When I run 'mocha tests' the tests pass.

--
Happy Hacking, MT
