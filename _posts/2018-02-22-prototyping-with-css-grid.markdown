---
layout: post
title: "Prototyping with CSS Grid"
permalink: "prototyping-with-css-grid"
date: 2018-02-22
categories: css
summary: How to easily prototype a website layout using css grid.
tags: [css, grid, css grid, prototype, webpage, website, layout]
---

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">In which we use the power of CSS Grid to build something useful...</span>

We've learned quite a bit about CSS Grid in just three short tutorials, and seen the various ways in which it can perform to meet our needs.  In today's post, we're going to actually build out a basic webpage layout from a mockup!

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">The Scenario</span>

If you've been employed as a front-end developer for any period of time, here's a common scenario that occurs:  Your boss/a client/designer/whomever is paying you, gives you the job of building out a webpage, and they provide you with a mockup of what the webpage should look like when it's done.  Sometimes it's very detailed, with specific colors and pixel sizes for headers and paragraph fonts, etc.  Other times it's very general.  I've even had a superior sketch out a basic design for a page on a napkin by pen and hand it to me.  No matter what sort of mockup you're provided, your job as a front-end developer depends on being able to build out webpages to the desired specifications.

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">The Mockup</span>

Here's an image of what a mockup of a very basic website might look like.  Even as bare bones as it is, it probably looks familiar to you, because you've seen this sort of layout on countless websites across the internet.  There's a header, a footer, a side menu for navigation, and a large area to hold the main content.  With CSS Grid, such a layout is quick and easy to build!

![simple webpage mockup](/assets/images/css_grid/prototype_mockup.png){: .center-image}

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">The HTML</span>

As with all other front-end projects, the first place we need to start is with our markup, in the form of HTML.  Here's what that might look like:

{% highlight html %}
<div class="container">
  <header class="header">header</header>
  <nav class="menu">menu</nav>
  <main class="content">content</main>
  <footer class="footer">footer</footer>
</div>
{% endhighlight %}

This probably looks about how you'd expect.  Nothing fancy going on here.

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">The Initial CSS Grid Setup</span>

{% highlight css %}
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-template-rows: 100px 400px 100px;
  grid-gap: 10px;
}
{% endhighlight %}

This should look very familiar to you at this point.  We declared that the container div in our markup is:

<span style="font-size: 1.25em;">1.</span> A grid <br>
<br>
<span style="font-size: 1.25em;">2.</span> With 12 columns, each occupying 1/12 of the available width of our browser window <br>
<br>
<span style="font-size: 1.25em;">3.</span> Three rows: the first 100px high, the second 400px, and the last 100px <br>
<br>
<span style="font-size: 1.25em;">4.</span> With gap between our columns and rows should be 10px

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Grid Template Areas</span>

The magic we need to really make this prototype come together quickly is a concept we haven't discussed yet, called template areas.

Take a look at this:

{% highlight css%}
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-template-rows: 100px 400px 100px;
  grid-gap: 10px;
  grid-template-areas:
    "h h h h h h h h h h h h"
    "m m c c c c c c c c c c"
    "f f f f f f f f f f f f"
}
{% endhighlight %}

Okay, that looks a little crazy at first!  Maybe even like a cat walked across my keyboard while I was working on this tutorial.  So what does this mean?  Well, the <code class="highlight-code">grid-template-areas</code> property is the only place in all of CSS where we create a visual representation of what an element should look like.  You'll notice it has twelve columns and three rows, just like we defined with <code>grid-template-columns</code> and <code>grid-template-rows</code>.  Each individual character represents a cell in our grid.

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Grid Areas</span>

The next thing we have to do is connect the values from the <code>grid-template-areas</code> property in our CSS to our HTML markup.  We can easily do that by using the <code>grid-areas</code> property, like so:

{% highlight css %}
  .header {
    grid-area: h;
  }
  .menu {
    grid-area: m;
  }
  .content {
    grid-area: c;
  }
  .footer {
    grid-area: f;
  }
{% endhighlight %}

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Note that I omitted some additional CSS that assigned colors to the grid areas, etc. because it doesn't deal directly with the grid.</span>

And here's our result:

![grid areas image](/assets/images/css_grid/grid_areas.png){: .center-image}

I think you'll agree it looks just like our original mockup.  Success!

But let's say our boss comes to us after we've prototyped our webpage and says the client decided they want the menu on the right hand side of the page.  Because we now know all about how the <code>grid-template-areas</code> property works, we can make the change in mere seconds!

{% highlight css%}
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-template-rows: 100px 400px 100px;
  grid-gap: 10px;
  grid-template-areas:
    "h h h h h h h h h h h h"
    "c c c c c c c c c c m m"
    "f f f f f f f f f f f f";
}
{% endhighlight %}

All we've done is move the 'm' <code>grid-template-areas</code> to the right side of the second row, and our menu is repositioned in a snap!

![repositioned menu](/assets/images/css_grid/repositioned_menu.png){: .center-image}

That's great, but the client has one more request: They'd like the header and footer of the site to be slightly wider than the menu and contents that are between the two.  How might we do that?  Believe it or not, it's just as easy.  All we need to do is leave a cell or two on the right and left of our <code>grid-template-areas</code> blank, and to do that we simply use a period in place of .

{% highlight css%}
.container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-template-rows: 100px 400px 100px;
  grid-gap: 10px;
  grid-template-areas:
    "h h h h h h h h h h h h"
    ". c c c c c c c c c m ."
    "f f f f f f f f f f f f";
}
{% endhighlight %}

![empty cells example](/assets/images/css_grid/empty_cells_example.png){: .center-image}

Right now our page layout looks pretty good at different browser window sizes because we defined our columns in fractions, which we know to be responsive.  However, things get a little cramped when the browser window gets too narrow.  Let's add some responsiveness to the mix by utilizing a CSS media query.  Let's say we want to give the content more width when the screen narrows to less than 740px wide, and we want to do that by placing the navigational menu just above it.  Here's how that might be done:


{% highlight css%}
@media screen and (max-width: 740px) {
  .container {
    grid-template-rows: 100px 50px 350px 100px;
    grid-template-areas:
    "h h h h h h h h h h h h"
    "m m m m m m m m m m m m"
    "c c c c c c c c c c c c"
    "f f f f f f f f f f f f";
  }
}
{% endhighlight %}

Before we look at the results in action, let's talk about what we did.  First, if you're not familiar with CSS media queries, all we did was use some additional syntax to write a CSS rule that will only apply to screens less than 740px in width.  You can read more about CSS media queries [here](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries).

So what does the new CSS say.  First, you'll notice the values of the <code>grid-template-rows</code> property have changed.  An additional row has been added.  The first row and last rows are still 100px each, just as before, but the two inner rows are 50px and 350px in height, respectively.  What I wanted to have happen on screens less than 740px in width is for the menu to move from the right side of screen to a new row just under the header, and span the full width of the grid.  You'll see the values of <code>grid-template-areas</code> have been changed to represent that behavior.  Because of that new row at 50px in height, I reduced the original height of the content row by the same amount, so that the total height of our explicit grid remains the same.

Check out the new behavior:

![css grid media query behavior](/assets/images/css_grid/css_grid_media_query.gif){: .center-image}

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Source Order Independence</span>

Notice how we didn't have to touch the HTML at all?  There's something really, really cool at play here, called source order independence.  We made all the layout decisions in the CSS, without regard to how the HTML is ordered.  We can move the contents of the grid around however we want, as long as they're child elements of a parent element with a display property set to a value of grid.  That's source order independence.
