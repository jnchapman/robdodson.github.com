---
layout: post
title: "nth-child is weird"
date: 2013-08-04 10:55
comments: true
categories: [CSS]
---

I ran into a CSS bug today and it brought up an interesting (and important) question: What's the difference between `nth-child` and `nth-of-type`?

<!--more-->

## Comparing two things or one

Take a look at this sample code to get a feel for what we're talking about.

``` html
<div>
  <p>This paragraph is not green :(</p>
  <p>This paragraph is green!</p>
</div>
```

``` css
p:nth-child(2) {
  background-color: green;
}
```

You'll notice that we're setting our second `p` element to have a `background-color` of `green`. To do this we use `p:nth-child(2)`. I think the way most people (myself included) would read that selector is "select the second child paragraph". But if we change the markup to look like this:

``` html
<div>
  <h1>Hello World!</h1>
  <p>This paragraph is not green :(</p>
  <p>This paragraph is green!</p>
</div>
```
Suddenly our green background moves to the wrong element. What gives?! As it turns out, `nth-child` counts all child elements regardless of what tag they are using.

As [Chris Coyier puts it on CSS-Tricks.](http://css-tricks.com/the-difference-between-nth-child-and-nth-of-type/)

{% blockquote %}
Our :nth-child selector, in "Plain English," means select an element *if*:

It is a paragraph element
It is the second child of a parent
{% endblockquote %}

Since we've added another child in the form of an `h1` tag, we need to now say `p:nth-child(3)` if we want to select the same element. In my mind that makes the `nth-child` tag extremely brittle and somewhat counterintuitive.

Thankfully there's an alternative in form of the `nth-of-type` selector.

``` css
p:nth-of-type(2) {
  background-color: green;
}
```

Again, quoting [Mr. Coyier](http://css-tricks.com/the-difference-between-nth-child-and-nth-of-type/):

{% blockquote %}
Our :nth-of-type selector, in "Plain English," means:

Select the second paragraph child of a parent
{% endblockquote %}

So `nth-of-type` gives us the functionality we were originally looking for and doesn't require us to change our markup if we add additional child elements which use different tags. That's pretty sweet. I wonder why I don't see `nth-of-type` used as often? It looks like they're both supported in Chrome/FF and IE9+. Maybe it's because `nth-child` initially seems easier to reason about although in actuality it's a little more complex.

If you want to play around with the idea [I've put together a codepen.](http://codepen.io/robdodson/pen/GzuKH) Enjoy!