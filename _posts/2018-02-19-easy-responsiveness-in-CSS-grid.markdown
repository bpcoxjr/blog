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

And here's what our grid looks like:

![grid-columns-rows](/assets/images/css_grid/grid_columns_rows.png){: .center-image}

* Remember, I omitted CSS for colors and centering the numbers, etc. from this post because those properties are irrelevant to how our grid performs.
