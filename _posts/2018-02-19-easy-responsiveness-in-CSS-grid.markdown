---
layout: post
title: "Easy Responsiveness in CSS Grid"
permalink: "easy responsiveness in css grid"
date: 2018-02-19
categories: css
---

# Continuing our css grid series...

In our last post we dove into learning how to implement a rudimentary CSS grid, talked about the differences between it and other popular grid systems provided by outside frameworks like [Bootstrap](https://www.getbootstrap.com/docs/4.0/layout/grid), and talked about its adoption and support rate in major browsers.

What you may have noticed about the grids we created in the examples was that they were not very responsive to changes in the size of our viewport.  Okay...there weren't responsive AT ALL.  Column widths were set in pixels in our CSS file, stayed fixed regardless of viewport width, and if we made the viewport small enough, some columns weren't visible at all.

Today, we're going to fix that, and it's much easier than you may imagine.  Let's get started...

---

Here's the HTML and CSS from our original grid:

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

{% highlight css %}
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 50px 50px;
}
{% endhighlight %}

And here's what our resulting grid looks like:

![grid-columns-rows](/assets/images/css_grid/grid_columns_rows.png){: .center-image}

* Remember, I omitted CSS for colors and centering the numbers, etc. from this post because those properties are irrelevant to how our grid performs.

No matter how we adjust our browser window size - wider, narrower, etc. our three columns are always going to be 100px wide.  That might work fine on a desktop computer.  But what if we're viewing our grid on a tablet or smart phone, where the dimensions of our browser window are far smaller?  Our 100-pixels-wide columns aren't very user friendly then, are they?

Let's change that.

First, let's shorten up how we establish our three columns and two rows, with a simple change.  Introducing repeat:

{% highlight css %}
.container {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(2, 50px);
}
{% endhighlight %}

Here we're telling the browser to display our grid exactly the same as before, we're just doing it slightly different.  Using repeat tells the browser to repeat (DUH!) what's inside the parentheses.  The first parameter we pass is the number of columns and rows we want to...wait for it...repeat (in our case 3 and 2, respectively), and the second parameter is the width (in the case of the columns, 100px) and height (in the case of the rows, 50px).  Easy, right?  But we still haven't tackled the obstacle of responsiveness!  Continuing on...

Let's assume there are, for whatever reason, use cases where we actually want columns to be fixed at certain pixel widths, and rows to be fixed at certain heights (Hey, it's the internet.  There are crazy use cases for everything!).  Well, we can achieve that and still have some responsiveness simply by adding one additional element to our above CSS.  Introducing, auto-fit:

Let's update our above CSS to include auto-fit so you can see how it works.

{% highlight css %}
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, 100px);
  grid-template-rows: repeat(2, 50px);
}
{% endhighlight %}

What we've done here is refrain from explicitly setting the number of columns to 3, and instead just told our browser to fit as many columns as it can at 100px wide, and once it runs out of room, simply wrap them on to an additional row as needed.

Here's a GIF to illustrate how that behavior works:

![auto-fit css grid](/assets/images/auto_fit.gif){: .center-image}
