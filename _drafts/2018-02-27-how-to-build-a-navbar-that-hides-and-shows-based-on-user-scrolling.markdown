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

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">2.</span>  It hides/shows based on the user's scrolling behavior, showing when the page initially loads, hiding when the user is actively scrolling down the page, and reappears only when the user begins to scroll back up the page.
<br>

To see the type of behavior I'm talking about, check out the nav bar on [my personal site](https://www.bpcoxjr.com).

The end benefit to the user here, other than it just looking cool, is that it gives more screen space for content.

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

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Note: Some CSS, such as font-family or font-size, has been omitted because it's not relative to the tutorial.  All code is, however, included in the Github repo, which is linked at the end of the article.</span>

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
<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">2.</span>  Its position is fixed.<br>
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

Here's what our nav bar looks like at this point:

![basic navbar](/assets/images/nav_bar_scrolling/navbar.png){: .center-image}

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
  }, 50);
{% endhighlight %}

Again, let's break down what's going on here.  <code>setInterval</code> is a built-in JavaScript method available to us.  Its behavior is such that it expects you to pass it a number that represents how often it should be called.  The number you pass is always in milliseconds.  See the <code>50</code> I pass at the end there?  It's 50 milliseconds.  If we only wanted to check every second, we'd pass a value of 1000 (1000ms = 1s).

You'll notice that every 250 milliseconds we also call a function called <code>hasScrolled()</code>.  Let's write that function now.

We're going to need a few more variables that we can store values in to make this all come together:

{% highlight JavaScript %}
var lastScrollTop = 0;
var delta = 5;
var navbarHeight = $('#nav-bar').outerHeight();
{% endhighlight %}

You'll see how each of these variables is used in a moment.  Right now, just notice that value of <code>lastScrollTop</code> is 0, <code>delta</code> is 5, and navbarHeight is set the outer height of our nav bar element, which we obtain by using jQuery to select the element by its ID, then obtain its full height by calling <code>outerHeight()</code>, another built-in jQuery method.  A quick console log of <code>navbarHeight</code> shows me a value of 67, which is the height I expect based on our discussion earlier about using the inspector in the dev tools to get the height of the element.

Now that we've got all of our variables in place, let's use see how they're used to make calculations that will determine when the nav bar is shown and hidden.

{% highlight javascript linenos %}
function hasScrolled() {
  var scrollTop = $(window).scrollTop();

  // Make sure user scrolls more than delta
  if (Math.abs(lastScrollTop - scrollTop) <= delta)
    return;

  // If user scrolls past the height of the navbar, remove class nav-bar-down add class nav-bar-up.
  if (scrollTop > lastScrollTop && scrollTop > navbarHeight) {
    $('#nav-bar').removeClass('nav-bar-down').addClass('nav-bar-up');
  }
  // If user is scrolling up, remove class nav-bar-up and add class nav-bar-down.
  else if (scrollTop + $(window).height() < $(document).height()) {
    $('#nav-bar').removeClass('nav-bar-up').addClass('nav-bar-down');
    }
  }

  lastScrollTop = scrollTop;
}
{% endhighlight %}

There is a lot to discuss here, so let's take a deep breath, and we'll go line by line to make sure we digest how it all works.

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">1.</span>  We declare our function, <code>hasScrolled()</code>, which we have already set to be called from <code>setInterval()</code> every 250 milliseconds.<br>

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">2.</span>  We declare a new variable, <code>scrollTop</code>, and we set it equal to the result of calling the jQuery method, <code>scrollTop()</code>, on the window object.  If you're not familiar with scrollTop, it's another built-in method jQuery offers us, which gets the vertical position of the scroll bar, in pixels, from the very top of the page.  Think of it as the total number of pixels that are hidden from view above the scrollable area.  You can read more about <code>scrollTop()</code> [here](https://api.jquery.com/scrollTop/).<br>

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">3.</span>  Our first <code>if</code> statement uses <code>Math.abs</code>, a built-in method of JavaScript's Math object, to get the absolute value of subtracting the value of <code>scrollTop</code> from <code>lastScrollTop</code>, then checks to see if the resulting number is less than or equal to the value of delta.  When our page first loads, the value of <code>lastScrollTop</code> is 0, and the value of <code>scrollTop</code> is 0 as well.  At the same time, the value of <code>delta</code>, which we set when we declared the variable, is 5.  Because 0 < 5, <code>return</code> is called, and the rest of our function's code is not parsed, so nothing happens.<br>

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">4.</span>  The next if/else statement is encountered only when the absolute value of the difference between <code>lastScrollTop</code> and <code>scrollTop</code> is greater than the value of <code>delta</code>.<br>

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">5.</span>  When the <code>if</code> portion of that second code block is reached, we first check to see if the value of <code>scrollTop</code> is greater than the value of <lastScrollTop>.  Remember what the two variables represent: lastScrollTop is initially declared by us to be 0, while we set <code>scrollTop</code> to basically measure the distance (measured in px) that the vertical scroll bar has traveled from the top of the document.  So because when the page first loads we set <code>lastScrollTop</code> to 0, this code, at least the first time it runs is just checking to see if the user has scrolled <span style="font-style: italic; text-transform: uppercase">at all</span>.  In a moment we'll talk about how it's measured for all other subsequent scrolls.  After that is checked, we check to see if <scrollTop> is greater than <navbarHeight>, which is easy to understand now: it is simply checking to see if the user has scrolled <span style="font-style: italic; text-transform: uppercase">completely</span> past the nav bar, so that is is no longer visible.<br>

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">6.</span> If - and only if - <span style="font-style: italic; text-transform: uppercase;">both</span> conditions are met (that's what the <code>&&</code> is checking: if condition 1 <span style="font-style: italic; text-transform: uppercase">and</span> condition 2 are true), the jQuery inside the <code>if</code> statement gets parsed.<br>

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">7.</span>  What that jQuery does is actually quite simple.  First, we select the nav bar by its ID, use jQuery's <code>removeClass()</code> method to remove the <code>nav-bar-down</code> class, then chain jQuery's <code>addClass()</code> method to add the <code>nav-bar-up</code> class, effectively hiding it from view by moving it 'up' the document the same number of pixels as its height (Remember, the <code>nav-down-class</code> has a <code>top</code> value of <code>0</code>, and the <code>nav-up-class</code>).<br>

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">8.</span>  The <code>else if</code> statement also compares two values to determine if its code block should be performed.  You'll notice that once again we are using a built-in jQuery method to obtain some values.  This time it's <code>height()</code>.  First we get the height of the <code>window</code> object (the height of your browser window) and add it to <code>scrollTop</code>.  Then we grab the <code>height()</code> of the <code>document</code> (the height of all of the contents of the page added together).  We compare the two values, and if the <code>document</code> has a higher value, we use jQuery one more time to reverse the CSS classes, which shows the nav bar again.  The reason for comparing the two values can be a little hard to wrap your head around.  I like to think of it this way: if the total height of the document is tall enough that it can be scrolled, this behavior will apply, otherwise there's no need for it.<br>

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">9.</span>  The last thing we do each time <code>hasScrolled()</code> gets called is to set <code>lastScrollTop</code> equal to <code>scrollTop</code>, which is the current position of the scrollbar on the page.  We do this because we are likely not at the very top of the page each time the function runs, and for our code to work properly we need to be able to accurately indicate where we were on the page the last time the function was called.<br>

Here's our complete JavaScript code:

{% highlight JavaScript %}
$(document).ready(function() {

  var didScroll;
  var lastScrollTop = 0;
  var delta = 5;
  var navbarHeight = $('#nav-bar').outerHeight();

  $(window).scroll(function() {
    didScroll = true;
  });

  setInterval(function() {
    if (didScroll) {
      hasScrolled();
      didScroll = false;
    }
  }, 50);

  function hasScrolled() {
    var scrollTop = $(window).scrollTop();

    // Make sure they scroll more than delta
    if (Math.abs(lastScrollTop - scrollTop) <= delta)
      return;

    if (scrollTop > lastScrollTop && scrollTop > navbarHeight) {
      $('#nav-bar').removeClass('nav-bar-down').addClass('nav-bar-up');
    } else if (scrollTop + $(window).height() < $(document).height()) {
      $('#nav-bar').removeClass('nav-bar-up').addClass('nav-bar-down');
    }

    lastScrollTop = scrollTop;
  }

});

{% endhighlight %}

Let's check out how the scrollbar behaves:

![nav behavior on scroll](/assets/images/nav_bar_scrolling/nav_scroll_behavior.gif){: .center-image}

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">One important note: In order for the scrolling behavior to work properly, your HTML document needs to be taller than your browser window.  While I didn't show it in the tutorial, I added several <code><div></code> elements to the HTML, underneath the <code><nav></code> element, with <code><h1></code> and <code><p></code> elements.  You probably noticed them in the above GIF.  This ensures there is plenty to scroll through to see the behavior.</span>

The entire source, which contains the additional <code><div></code> elements is available on [
my Github page](https://github.com/bpcoxjr/navbar_scrolling).  Feel free to clone it and play around!

Until next time, happy coding!
