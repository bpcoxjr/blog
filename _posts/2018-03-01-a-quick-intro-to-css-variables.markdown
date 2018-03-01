---
layout: post
title: "A Quick Intro to CSS Variables"
permalink: "a-quick-intro-to-css-variables"
date: 2018-03-01
categories: css
summary: A quick introduction to get up and running with css variables
tags: [front end development, html, css]
---

# <span style="color: #ac0863;">A brief, but informative look.</span>

<span style="font-weight: bold; font-size: 1.25em; color: #ac0863;">The History</span>

CSS variables have been around for quite a while now.  They were originally introduced to the specifications in 2012 by the [W3C](https://www.w3.org).  However, like any new advancement in the digital world, it took some time before the addition of variables into pure CSS was adopted by all the major browsers.  Initially, only Chrome and Firefox supported CSS variables.

But in 2014, the syntax for CSS variables improved.  This prompted Mozilla, makers of Firefox, to push forward with their support.  Meanwhile Google, the makers of Chrome, pulled most of their support, opting to wait for the basics of the syntax to be agreed upon before they went all in with their support.  Even as recent as 2015 support across all major browsers hovered around a lowly 9%.  Sometime in 2016, most of the major browser creators jumped on board, and at the time of this posting world-wide browser support stands at [87%](https://www.caniuse.com/#search=css%20variables)!

![CSS Variables Browser Support Rate](/assets/images/css_variables/css_variables_support.png){: .center-image}

<span style="font-weight: bold; font-size: 1.25em; color: #ac0863;">Why CSS Variables?</span>

If you've ever used a style sheet language like [Sass](https://sass-lang.com) or [Less](https://lesscss.org), you already know about many of the features they offer, and how convenient they can be.  Among their many features is the ability to store a CSS property and its value, like <code>font-size</code> or <code>color</code>, in a variable of our choosing, then use that variable wherever we want throughout our style files.  And if we need to change a property's value, we only have to do it in one place, which saves the time and effort of having to search through an entire file.  With the ability to use variables this way already in existence, why did we need CSS variables, and what is their benefit?

Learning the syntax of Sass or Less is simple.  If you have much familiarity with pure CSS at all, you can learn Sass or Less in a couple of hours.  However, learning to compile them can be a real pain.  If you've never used them, your'e probably wondering what I'm even talking about when I refer to having to compile them.  While we as users can understand their respective syntaxes, browsers are not equipped to understand what they mean, and therefore we either need to find, install, and learn how to use a plug-in for our text editor that can handle the conversation for us, or we need to take the time to learn how to use a build tool like [Gulp](https://gulpjs.com), which is great for your workflow, but can take a considerable amount of time to learn and set up in your project.  And if your project is relatively simple, it can be overkill.  One of the great benefits of CSS variables is that we need no special tools to transpile them into something browsers can understand.

Another advantage of CSS variables is that they have access the DOM (document object model), whereas Sass or Less Variables do not.  We will talk more about what this means and how it benefits us as developers, momentarily.

<span style="font-weight: bold; font-size: 1.25em; color: #ac0863;">How to Declare a CSS Variable</span>

Declaring a CSS variable is a little bit different, because the first step, before we even write it, is to decide what its scope should be (i.e. should it be a global variable, and therefore available throughout the doccument?  Or should it be a local variable, scoped only to the element its declared on?)

<span style="font-weight: bold; font-size: 1em; color: #ac0863;">Global Variables</span>

If we want it to be a global variable, we declare it on the <code>:root</code>, like so:

{% highlight css %}
:root {
  --primary-color: #FFDC00;
}
{% endhighlight %}

This probably looks very familiar, with the exception of one thing: the two dashes.  You can name a variable whatever you want, the only requirement is that it be prefixed with <code>--</code>.

To access the variable after declaring it, we use the <code>var()</code> function.  Here's what that looks like:

{% highlight css %}
.header {
  color: var(--primary-color);
}
{% endhighlight %}

We simply pass the variable we declared to the <code>var()</code> function.  Easy, right?

<span style="font-weight: bold; font-size: 1em; color: #ac0863;">Local Variables</span>

The CSS variables spec also gives us the ability to declare variables that are local in scope.  This means they are only accessible to the element they are declared on, plus any children.  This makese sense if you have, say, a color you are only using on one element in an application, and nowhere else.

Let's say we have a div with a class of container:

{% highlight html %}
<div class="container">
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
</div>
{% endhighlight %}

And we want to write a local variable available to just this div:

{%highlight css %}
.container {
  --border-color: #808080;
}

.container {
  border: 1px solid var(--border-color);
}
{% endhighlight %}

There you have it: a variable that stores a color, and is only accessible to <code>.container</code>.  If we were to try to use the variable on any other element in our application, the browser would simply ignore it when parsing the CSS files.

<span style="font-weight: bold; font-size: 1.25em; color: #ac0863;">DOM Access</span>

As I mentioned earlier, a benefit of CSS variables is their access to the DOM.  This means we can do things like update the value of a CSS variable directly from the DOM.  Let's say we want to change font sizes based on screen width.  Instead of having two different variables for a primary <code>font-size</code>, we can just update the value of the variable that stores that size.

Take a look:

{% highlight css%}
:root {
  --primary-font-size: 12px;
}

@media screen and (min-width: 720px) {
  :root {
    --primary-font-size: 16px;
  }
}
{% endhighlight %}

By writing one simple media query, we're able to update the <code>font-size</code> across our entire application to handle changes in the browser window size of our users!  I think you'll agree that was quick and easy.

Well, that's it for our quick introduction to CSS variables.  Even by just dipping our toe in the pool, we've learned how powerful they can be, but we've only scratched the surface.  In our next post, we'll take a look at how to interact with CSS variables via JavaScript.

As always, until next time, happy coding...
