---
layout: post
title: "Explicit vs Implicit CSS Grid"
permalink: "explicit-vs-implicit-css-grid"
date: 2018-02-20
categories: css
---

Let's reflect on how we've defined grids in CSS so far.  We've created a parent/container element to hold child items, and we've placed those child items into cells that we define via grid columns and rows.  That's worked fine for us so far.  However, one of the great strengths of CSS Grid is the ability for the grid to adapt to its items.

This adaptability is managed by what is known as the <span style="font-style: italic;">explicit</span> and <span style="font-style: italic;">implicit</span> grid.

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">The Explicit Grid</span>

The explicit grid is just what it sounds like: it's the grid we <span style="font-style: italic;">explicitly</span> define in our CSS file.  When we defined our grid in the early stages of our [responsive grid tutorial](https://www.displayblog.io/easy-responsiveness-in-css-grid), we did so by defining very specific columns and rows.  Here's how we did that:

{% highlight css %}
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-template-rows: repeat(2, 50px);
}
{% endhighlight %}

We told the browser we want a grid that establishes its number of columns based on how many it can fit within the viewport, as long as they're at least 150px wide, and if there's extra space they should be 1 fraction wide, meaning each should occupy an equal amount of the available width.  We also told the browser to establish <span style="font-style: italic;">exactly</span> two rows that are each <span style="font-style: italic;">exactly</span> fifty pixels high.  Those two lines of CSS are where we defined the explicit grid.  

Now lets take a look at its behavior again:

![minmax grid usage](/assets/images/minmax_usage.gif){: .center-image}

Everything behaves as we've learned it should - up until the point we make our viewport too narrow to support all six of our grid items at a minimum of 150px wide on our two defined columns.  But it still works!  At its smallest, our grid can only fit two grid items per row, so once it reaches items five and six, it wraps them onto a new third row, without us even telling it to.  This is an example of the <span style="font-style: italic;">implicit</span> grid at work.

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">The Implicit Grid</span>

If you look really closely at the GIF above, you'll notice the grid items are slightly taller than the grid items on our two defined grid rows, which are 50px in height.  This is because when the implicit grid creates new rows or columns to hold grid items, it takes a look at the contents of the grid item, and sizes it as it sees fit, basically allotting just enough space for that content, while still looking acceptable.  If we don't explicitly define enough space for all the grid items, and the implicit grid kicks it, it kind of does it's own thing.  However, we can change this behavior easily.

Enter grid-auto-rows and grid-auto-columns:

{% highlight css%}
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(2, 50px);
  grid-auto-columns: 250px;
  grid-auto-rows: 50px;
}
{% endhighlight %}

In this particular example, the grid-auto-columns property doesn't come into play, but it can't hurt to set both of these properties when building out our grid, just to handle any future 'what if' scenarios.  What does come into play is the grid-auto-rows setting.  Remember that before we set a value for this property, the implicit grid was just doing its own thing, and the grid items it added to the new third row differed in height from our first two rows.  By setting the value of grid-auto-rows at 50px, any new rows past the original two we explicitly defined will match their height.

Let's check out our result, paying special attention to what happens when items five and six wrap to a new implicit third row:

![implicit row usage](/assets/images/implicit_rows.gif){: .center-image}

What if instead of having the implicit grid create a new third row to hold items five and six, we wanted them to be added to a new implicit column?  We can easily make that specification as well, using the grid-auto-flow property, which can be set to a value of column or row.

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Wrap Up</span>

We haven't covered all the concepts of the explicit vs implicit grid, but we've learned enough to be dangerous.  To learn more, check out Mozilla's guide [here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Auto-placement_in_CSS_Grid_Layout).

Stay tuned for our next post, where we'll take a look at how to prototype a basic webpage layout from a mock-up, using CSS Grid!
