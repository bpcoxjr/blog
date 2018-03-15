---
layout: post
title: "Using JavaScript to Interact with CSS Variables"
permalink: "using-js-to-interact-with-css-variables"
date: 2018-03-15
categories: css, javascript
summary: How to use JavaScript to interact with CSS variables.
tags: [front end development, html, css]
---

# <span style="color: #ac0863;">Continuing our introduction...</span>

Welcome to another tutorial.  Today we're going to talk about interacting with CSS variables using JavaScript.  If you'll recall from our [introduction to CSS variables post](http://www.displayblog.io/a-quick-intro-to-css-variables), one of the big advantages of the advent of CSS variables is their access to the DOM.  We looked at how this meant we could easily update the value of a variable, using a media query as an example.

Additionally, because of their DOM access, we can interact with CSS variables using JavaScript.  Let's take a look at how we might do that, using just a little bit of code.

{% highlight JavaScript %}
let root = document.querySelector(':root');
let rootCSS = getComputedStyle(root);
let primaryColor = rootCSS.getPropertyValue('--primary-color');
{% endhighlight %}

Okay, let's look at what is going on here.

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">1.</span>We use the built-in JS method <code>querySelector</code> to select the <code>:root</code>, which is the highest level parent element present in the DOM.  This is almost always going to be <code><html></code>.  

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">2.</span>  We use another built-in JS method, <code>getComputedStyle()</code> to grab all the CSS styles on the page.

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">3.</span>We grab the <code>--primary-color</code> variable and store it in a local variable so that we can operate on it.

If we were to run <code>console.log(primaryColor)</code> the hex value of the color would be printed to the console (i.e. <code>#ffffff</code> if it were white).

Changing the value of <code>--primary-color</code> couldn't be easier using yet another built-in JS method, <code>setProperty()</code>.  Here's how:

{% highlight JavaScript %}
  root.style.setProperty('--primary-color', '#000000')
{% endhighlight %}

So why would we want to do something like this?  I can give you a real world, popular example:  The Twitter app on your phone.  The settings have a 'Night Mode' switch you can use to make it easier to read in the dark.  All it does is swap a white background for a black one, and black print for white, and BOOM!...it's easier on the eyes.

Using the above code one could easily create a <code>html</code> toggle that calls a function that runs the above code when clicked, thus changing the primary color, then reversing the process when clicked again.  

There are of course countless other use cases for manipulating CSS variables in the DOM with JavaScript.  Give it a try on your next project!
