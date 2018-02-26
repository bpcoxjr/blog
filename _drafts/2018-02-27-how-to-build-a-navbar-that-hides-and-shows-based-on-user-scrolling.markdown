---
layout: post
title: "How to Build a Navbar that Hides or Shows Based on User Scrolling"
permalink: "how-to-build-a-navbar-that-hides-or-shows-based-on-user-scrolling"
date: 2018-02-27
categories: [html, css, javascript]
summary: Navbar that hides and shows based on user scrolling on a website
tags: [front end development, html, css, javascript, responsiveness]
---

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Welcome to another tutorial here at display: blog!</span>

If you're anything like me, you often see cool features and design behaviors on websites that catch your eye, and make you think to yourself "How'd they do that?"  For me, one of those things I saw across the web, and sought out learning how to build, was a nav bar that does a couple of really cool things:

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">1.</span>  It sticks to the top of our screen, no matter where we are on the page.<br>
<br>
<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">2.</span>  It hides/shows based on the user's scrolling behavior, showing when the page initially loads, hides when the user is actively scrolling down the page, and reappears only when the user begins to scroll back up the page.
<br>

To see the type of behavior I'm talking about, check out the nav bar on [my personal site](https://www.bpcoxjr.com).

Today, we're going to build this kind of nav bar.  Let's get started...

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">The HTML</span>

First, we're going to need to build the markup for our nav bar.  There's nothing too special going on here.  The most important thing to notice is that we've given our nav bar an ID: <code><nav id="top-bar"></code>.  This is so that when we incorporate JavaScript to obtain the hiding/showing behavior we're after, we can easily locate and select our nav bar to apply the magic.

{% highlight HTML %}
<nav class="nav-bar nav-bar-down" id="nav-bar">
  <div id="topbar-responsive" class="topbar-responsive-links">
    <div class="top-bar-left">
      <ul class="menu simple vertical medium-horizontal">
        <li><a href="">Home</a></li>
        <li><a href="">Link 1</a></li>
        <li><a href="">Link 2</a></li>
      </ul>
    </div>
  </div>
</nav>
{% endhighlight %}

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">The CSS</span>

Next, we're going to apply some basic CSS to give our nav bar some nice, simple styling.

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Note: Some CSS, such as font-family or font-size, has been omitted because it's not relative to the tutorial.</span>

Here's the CSS for the nav bar:

{% highlight css %}
.navbar {
  width: 100%;
  position: fixed;
  z-index: 500;
  transition: all 0.5s ease-in-out;
  background: rgba(0, 0, 0, 0.7);
  padding: .5em .75em;
  box-sizing: border-box;
}
{% endhighlight %}

A few things to note here:

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">1.</span>  We set width to 100%, so the nav bar spans the full width of our browser window.<br>
<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">2.</span>  Its position is fixed.
<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">3.</span>  It has a high <code>z-index</code> value.  This is so that when it is supposed to be visible, we can ensure it overlays all other elements on the page and isn't hidden behind any other elements (The value of 500 is arbitrary.  Just make sure you set <code>z-index</code> to a number higher than that of any other elements).<br>
<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">4.</span>  It has a transition value set, which allows it to have a nice smooth animation when it alternates between being hidden and being shown.  Here I set it to half a second each way.<br>
<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">5.</span>  This is just a personal preference, but notice how when setting the <code>background</code> to black, I set the fourth value to something less than 1, which allows the nav bar to be slightly transparent when visible, so that the element(s) it covers are just barely visible underneath.  Again, this is just a personal preference, and I don't use it all the time, but I like to use it in many cases.  I encourage you to play around with the actual number and see what you like.<br>

Next up is the CSS for the <code>nav-bar-links-container</code>.  In our example, I wanted all links to be displayed on the right side of the nav bar, so I used <code>float</code> like so:

{% highlight css %}
.nav-bar-links-container {
  float: right;
}
{% endhighlight %}

For the links themselves, we want to override some default behavior:

{% highlight css%}
.nav-bar-link {
  list-style-type: none;
  display: inline-block;
  padding: 0 10px;
}
{% endhighlight %}

To get rid of the bullet points that CSS adds by default to list items, I set <code>list-style-type: none;</code>.  I want the links to be displayed side-by-side, so I set <code>display</code>? to a value of <code>inline-block</code>.  And to give each individual link some room to breath, I give them some <code>padding</code>.

And finally, here's the CSS for the links themselves:

{% highlight css%}
.nav-bar-link a {
  color: #fff;
  text-decoration: none;
}
{% endhighlight %}

The <code>color</code> is irrelevant, but note that I set <code>text-decoration: none</code>.  This overrides the links from being underlined by default, which in my opinion is just ugly.

Now let's talk about some really important css that is going to help make the magic happen.  You may have noticed that in addition to a class of <code>nav-bar</code> our nav bar element also has a class of <code>nav-bar-down</code> that we haven't discussed yet.  Here's the CSS for that class: <br>

{% highlight css %}
.nav-bar-down {
  top: 0;
}
{% endhighlight %}

Because our nav-bar CSS includes <code>position: absolute;</code> we can apply the top property to move the element around the page.  The <code>top</code> property sets the top edge of an element to a unit above or below the top edge of its nearest position ancester.  Our nav bar has no anscestors, so <code>top: 0;</code> positions the top edge of the nav bar to the very top edge of our browser window.  The important thing to notice here is that we include the class in our HTML up front, so that it is applied to our nav bar when the page initially loads.

There's one more important CSS class to establish, and its the class that will allow our nav bar to be hidden from view.  Here is is:

{% highlight css%}
.nav-bar-up {
  top: -67px;
}
{% endhighlight %}

This class establishes a class that does one thing: change the value of our nav-bar's top property, thus hiding it from view (remember it is initially set to 0 because the class <code>nav-bar-down</code> is applied).  In this example, <code>top</code> is set to <code>-67px</code>.  To arrive at this number, I added the height of the element plus any top and bottom padding, border top and bottom, and margin top and bottom.  An easy way to do this is to use the dev tools in your browser to inspect the element for each of these values.  The inspector showed me that my element was 51px in heigh, with additional padding of 8px top and bottom.

51 + 8 +8 = 67

Setting <code>top: -67px;</code> moves the nav bar element up by the total value of its height, taking it completely out of view.

So we've got our HTML and CSS taken care of.  Cool.  But how do we make the whole thing work?  How do we listen for a user to scroll up and down the page, then alternately add and remove the <code>nav-bar-down</code> and <code>nav-bar-up</code> classes to hide and show the nav bar, based on that user scrolling behavior?  We need JavaScript!

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">The JavaScript</span>

There are quite a steps and processes that must occur to achieve the behavior we desire, but it's not as difficult as you might think.  We're going to use a combination of plain old, vanilla JavaScript and jQuery to make it all happen.  Why jQuery?  Because it has some built-in methods that allow us to write less code overall than if we used only JavaScript.

If you aren't familiar with jQuery, start [here](https://jquery.com).

The first thing we need to do is establish a way to check if a user is scrolling on the page.  Because there are only two possible outcomes (a user is either scrolling or they aren't) we need a variable to store a boolean (true or false) value.  Here it is:<br>

<code>var didScroll</code>

Notice we are not setting its value initially, we are simply declaring the variable so later we can store and change its value.  We want the value of <code>didScroll</code> to be set to true when the user scrolls.  Here's how we can use jQuery to do that:

{% highlight JavaScript %}
$(window).scroll(function(event) {
  didScroll = true;
});
{% endhighlight %}

Let's talk about how this works.  First, we select the window object, and use jQuery's built-in <code>scroll</code> method to listen for the user to scroll, then establish a function to set the value of <code>didScroll</code> to true.  Easy enough.

The next thing we need to do is consider the way people behave when using a webpage.  They might read for a moment, scroll, then stop to read more, then scroll again.  For our nav bar to be able to hide or show itself at again given time, we need to constantly be listening for the user to scroll.  To do that, we can use JavaScript's <code>setInterval</code> method:

{% highlight JavaScript %}
setInterval(function() {
  if (didScroll) {
    hasScrolled();
    didScroll = false;
  }
  }, 250);
{% endhighlight %}

Again, let's break down what's going on here.  <code>setInterval</code> is a built-in JavaScript method available to us.  Its behavior is such that it expects you to pass it a number that represents how often it should be called.  The number you pass is always in milliseconds.  See the 250 I pass at the end there?  It's 250 milliseconds, or one quarter second.  If we only wanted to check every second, we'd pass a value of 1000 (1000ms = 1s).

You'll notice that every 250 milliseconds we also call a function called <code>hasScrolled()</code>.  Let's write that function now.

We're going to need a few more variables that we can store values in to make this all come together:

{% highlight JavaScript %}
var lastScrollTop = 0;
var delta = 5;
var navbarHeight = $('#nav-bar').outerHeight();
{% endhighlight %}

You'll see how each of these variables is used in a moment.  Right now, just notice that value of <code>lastScrollTop</code> is 0, <code>delta</code> is 5, and navbarHeight is set the outer height of our nav bar element, which we obtain by using jQuery to select the element by its ID, then obtain its full height by calling <code>outerHeight()</code>, another built-in jQuery method.  A quick console log of <code>navbarHeight</code> shows me a value of 67, which is the height I expect based on our discussion earlier about using the inspector in the dev tools to get the height of the element.

Now that we've got all of our variables in place, let's use see how they're used to make calculations that will determine when the nav bar is shown and hidden.

{% highlight JavaScript %}
function hasScrolled() {
  var scrollTop = $(window).scrollTop();

  // Make sure user scrolls more than delta
  if (Math.abs(lastScrollTop - st) <= delta)
    return;

  // If user scrolls past the height of the navbar, remove class nav-bar-down add class nav-bar-up.
  if (scrollTop > lastScrollTop && scrollTop > navbarHeight) {
    $('#nav-bar').removeClass('nav-bar-down').addClass('nav-bar-up');
  }
  // If user is scrolling up, remove class nav-bar-up and add class nav-bar-down.
  else {
    if (scrollTop + $(window).height() < $(document).height()) {
      $('#nav-bar').removeClass('nav-bar-up').addClass('nav-bar-down');
    }
  }

  lastScrollTop = scrollTop;
}
{% endhighlight %}

There is a lot to discuss here, so let's take a deep breath, and we'll go line by line to make sure we digest how it all works.
