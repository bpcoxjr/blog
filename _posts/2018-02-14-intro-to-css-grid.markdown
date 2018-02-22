---
layout: post
title: "Intro to CSS Grid"
permalink: "intro-to-css-grid"
date: 2018-02-19
categories: css
---

# Welcome to the very first tutorial here at display:blog!

As I'm sure you've gathered from the title of this post, we're going to get our feet wet with CSS grid.  Why CSS grid?  Because having a firm grasp on a grid system is fundamental to building modern, responsive websites that look good across screens of all sizes, and CSS grid (in my opinion) is not only the most powerful option available today, but is also easy to learn.

If you've dabbled in front-end development for any amount of time, you're probably familiar with multiple other grid systems.  There is no shortage of available options.  [Bootstrap](https://www.getbootstrap.com/docs/4.0/layout/grid/) is probably the most popular, but others like [Foundation](https://foundation.zurb.com/grid.html) and [Bourbon Neat](https://neat.bourbon.io) have also gained some traction in the fast-changing front-end world.  With such a crowded grid-focused space, was baking grid capability directly into CSS really needed?  YES!

CSS grid has gained major traction to date, with a quick check of its adoption rate among major browsers at [almost 87%](https://caniuse.com/#feat=css-grid)

Adding grid capability to plain old CSS allows developers to break free from having to include entire third-party libraries in their web projects.  

No more linking to Bootstrap in the head of your HTML, or downloading Neat via NPM, Bower, etc.

No more including those ugly class names that usually come with other grid systems in your HTML.  This means keeping everything related to the CSS in the actual CSS file, not the HTML markup.

No more being handcuffed by Bootstrap's 12 column setup.  Want a grid with just 7 columns?  Go right ahead.  

All of these differences I'm pointing out mean one thing: more efficiency and more flexibility for you, the developer.

Okay, enough talking about why CSS grid is awesome.  Let's dig in and experience its advantages!

----

<span style="font-weight: bold; font-size: 1.25em; color: #ac0863">Defining a Grid</span>

There are very few hard and fast rules when it comes to the initial setup of a CSS grid.  In fact, there are only two.

First you need a parent element - a "wrapper" div to serve as a container.  And inside that container, you place your child elements, or grid items.  Below is a very basic example.  We have a parent div, with a class of "container" (you can name the class whatever you want), and inside we have six children div elements.

{% highlight html %}
<div class="container">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div>
{% endhighlight %}

Okay, cool.  But this is just basic HTML.  How do we give it magical CSS grid powers?  Remember how I mentioned earlier one of the advantages of CSS grid over other options like Bootstrap is that we keep the CSS in the CSS file?  Let's take a look at the CSS and learn how to get this CSS grid going.

{% highlight css %}
.container {
  display: grid;
}
{% endhighlight %}

Congratulations.  You just created your first CSS grid.  Let's see what it looks like (Note that I have included other CSS that you will not see here, just to make it prettier, but that CSS has no effect on grid layout or behavior).

![intial-grid](/assets/images/css_grid/initial_grid.png){: .center-image}

Right now you're probably thinking to yourself that this doesn't look like any grid you've ever seen.  Well, that's because we haven't defined any real rules to what we want our grid to look like, and how we want it to behave.  What you're seeing right now is the default layout of a CSS grid.  We haven't defined any columns at all, so the six rows we defined are taking up the entire width of the browser.  Let's take a look at how we can change that by adding a rule that defines our columns and rows.

<span style="font-weight: bold; font-size: 1.25em; color: #ac0863">grid-template-columns/grid-template-rows</span>

{% highlight css %}
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 50px 50px;
}
{% endhighlight %}

So what have we done here?  We've added a property called <code>grid-template-columns</code> and defined three columns, each 100px wide.  We've also added another property, <code>grid-template-rows</code>, and defined two rows, each 50 pixels in height.

This is what you should see in the browser:

![grid-columns-rows](/assets/images/css_grid/grid_columns_rows.png){: .center-image}

Easy enough.  Let's change the values of our two new properties, just to make sure we understand the relationship.

{%highlight css %}
.container {
  display: grid;
  grid-template-columns: 200px 100px 200px;
  grid-template-rows: 100px 50px;
}
{% endhighlight %}

![columns-rows-adjusted](/assets/images/css_grid/columns_rows_adjusted.png){: .center-image}

Just as we'd expect, the first and third columns, at 200px wide, are twice as wide as the second column, at 100px wide.  And at 100px in height, our first row is twice as tall as our second row, at 50px. Okay, cool.  But what if we want our grid items to be wider than the column they're in, or taller than their row?  Enter the <code>grid-column</code> and <code>grid-row</code> properties.

<span style="font-weight: bold; font-size: 1.25em; color: #ac0863">grid-column-start/grid-column-end</span>

{%highlight css %}
.item1 {
  grid-column-start: 1;
  grid-column-end: 3;
}
{% endhighlight %}

(While it's not present in our initial HTML screenshot, I added a class of item1, item2, and so on to each grid element so that each can be individually targeted with CSS rules.)

Our two above CSS rules can be simplified, written as a single shorthand rule, like so:

{%highlight css %}
.item1 {
  grid-column: 1 / 3;
}
{% endhighlight %}

![column-start-end](/assets/images/css_grid/column_start_end.png){: .center-image}

Let's talk a little bit about what's going on here.  Setting <code>grid-column-start</code> to a value of 1 means we want our item to start at the left edge of the first column (the first grid column line starting at the left edge), while setting <code>grid-column-end</code> to a value of 3 means go to the 3rd defined column, which in this case is the left edge of the third column (each column has a left and right edge).  If we wanted item1 to span the full width of the grid, we would set <code>grid-column-end</code> to a value of 4.  Additionally, notice how although we have only defined two rows in our CSS rules, items wrap onto the next available row, and in the case of item6, a whole new row altogether.  You'll also notice item6 inherited the height that we defined for our first grid row.

The <code>grid-row-start</code>/<code>grid-row-end</code> and short-hand <code>grid-row</code> properties work similarly.

{% highlight css %}
“.item1 {
  grid-row: 1 / 3;
}”
{% endhighlight %}

![grid-row](/assets/images/css_grid/grid_row.png){: .center-image}

To confirm our grasp of how these CSS grid properties work, let's use a mix of <code>grid-column</code> and <code>grid-row</code> on our grid.

{% highlight css %}
.item1 {
  grid-column: 1 / 3;
}
.item3 {
  grid-row: 2 / 4;
}
.item4 {
  grid-column: 2 / 4;
}
{% endhighlight %}

Here's our result:

![grid-column-grid-row-combo](/assets/images/css_grid/grid_column_grid_row_combo.png){: .center-image}

Something to notice here is that the grid items that have no specific rules written for them (items 2, 5, and 6) adapt to the rules of the other grid items, and take up the remaining space.

While we're on the topic of talking about the <code>grid-column</code> and <code>grid-row</code> properties, here's a quick tip if you want a grid item to span the full width of the grid, without having to count the number of grid column lines.  Set the first <code>grid-column</code> value to 1, and the second to -1.

{% highlight css %}
.item1 {
  grid-column: 1 / -1;
}
{% endhighlight %}

Here's the result, without changing anything else:

![grid-column-trick](/assets/images/css_grid/grid_column.trick.png){: .center-image}

Our first grid item spans the width of the entire grid, and all other grid items adjust accordingly.

<span style="font-weight: bold; font-size: 1.25em; color: #ac0863">grip-gap</span>

So far each of the grid items in our examples have been pretty cozy with each other.  That's all good and well, but what if we want a little breathing room between items?  Meet <code>grid-gap</code>.  <code>grid-gap</code> by default has a value of 0 unless otherwise defined in the CSS.  Aside from being set to 0, it can be a percentage, ems/rems, and pixels.  And which one you choose affects the gap's behavior.

Let's take a look what happens if we set <code>grid-gap</code>'s value to a percentage:

{% highlight css %}
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 50px;
  grid-gap: 10%;
}
{% endhighlight %}

![grid-gap-as-a-percentage](/assets/images/css_grid/grid_gap_percent.png){: .center-image}

Is the behavior what you expected?  Here's what's going on when we assign a percentage value to the <code>grid-gap</code> property: <code>grid-gap</code> establishes a "gutter" between grid columns that is relative to the dimension of the element.  Simplified: the white space we see between each of the columns is equal to 10% of the total width of the entire grid.

Let's set it to a pixel value:

{% highlight css %}
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 50px;
  grid-gap: 10px;
}
{% endhighlight %}

![grid-gap-as-pixels](/assets/images/css_grid/grid_gap_pixels.png){: .center-image}

Right away you'll notice the difference: assigning a pixel value to <code>grid-gap</code> sets a gap width to columns AND rows. Using em/rem units beaviors similarly.

Let's say we want to get really fancy and have wider gaps between columns than rows.  We decide we want 30px between columns and just 5px between rows.  That's easily attainable, like so:

{% highlight css %}
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 50px;
  grid-gap: 5px 30px;
}
{% endhighlight %}

![shorthand_grid_gap_rows_and_columns](/assets/images/css_grid/shorthand_grid_gap_rows_columns.png){: center-image}

I think just by seeing the result of assigning two values to the <code>grid-gap</code> property we can discern what's going on.  The first value is the gap we want between rows, and the second is the gap we want between rows.  If you'd prefer to be more specific, you can write these two <code>grid-gap</code> properties separately, but to me the shorthand value is so much cleaner.  Here's what that would look like:

{% highlight css %}
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 50px;
  grid-row-gap: 5px;
  grid-column-gap: 30px;
}
{% endhighlight %}

Either way, the result is the same.

----

That's it for our introduction to CSS grid.  As you can see, it's pretty neat, and easy to get started with.  I bet you're wondering where the responsiveness comes in.  We'll take a look at that in our next tutorial.

Until next time, happy developing...
