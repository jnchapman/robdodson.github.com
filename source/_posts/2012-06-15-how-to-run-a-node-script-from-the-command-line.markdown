---
layout: post
title: "How to Run a Node Script from the Command Line"
date: 2012-06-15 19:46
comments: true
categories: [Chain, Node, NPM, CLI]
---

This post is going to be short and sweet because I have to help my lady pack for her big trip to Germany. Over the past few days I've been messing around with command line tools written in Ruby so today I decided to give it a shot in Node.

<!--more-->

We're going to start small in this first post and just get a little script running. After that we'll step it up so it can be distributed using NPM, [just like we did with our previous Ruby gem.](http://robdodson.me/blog/2012/06/14/how-to-write-a-command-line-ruby-gem/)

## First write some codez

Make a new directory called `compliment` and create two files inside of it: `comliment.js` and `package.json`.

In `compliment.js` we're just going to print out some kind words.

``` js compliment/compliment.js
#! /usr/bin/env node

console.log('you. are. AWESOME!');
```

Simple enough right? Just make sure you include that shebang up at the top which directs the system to use Node to execute our script.

## Package it up

Ok now that we have our little script we'll give its `package.json` some love.

``` js compliment/package.json
{
    "name": "compliment",
    "version": "0.0.1",
    "description": "Tell us how awesome we are.",
    "preferGlobal": "true",
    "bin": { "compliment": "compliment.js" },
    "author": "Rob Dodson",
    "engines": { "node": "*" }
}
```

Most of that should be self explanatory. The key aspect is the `bin` section where you tell it to translate `compliment` into `compliment.js`. To install it all we have to do is run `npm link`. After you've done that you should be able to type `compliment` and hear how awesome you are!

Keep in mind this isn't distributable just yet, we'll work on that tomorrow. Till then have fun playing with your new powers :D

- Rob

You should follow me on Twitter [here.](http://twitter.com/rob_dodson)

<ul class="personal-stats">
    <li>Mood: Awake, Antsy</li>
    <li>Sleep: 6</li>
    <li>Hunger: 2</li>
    <li>Coffee: 0</li>
</ul>