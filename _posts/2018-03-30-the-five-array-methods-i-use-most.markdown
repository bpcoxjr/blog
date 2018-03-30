---
layout: post
title: "The JavaScript Array Methods I Use Most"
permalink: "the-javascript-array-methods-i-use-most"
date: 2018-03-26
categories: javascript
summary: An introduction to css grid.
tags: [arrays, javascript, tutorial, guide]
---

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">A Quick Look at Some Powerful JavaScript Array Methods</span>

If you've been developing with JavaScript for any measurable amount of time, you should be familiar with arrays.  Arrays conveniently let us store ordered collections.

An array can be declared two ways:

{% highlight JavaScript %}
let arrayOne = new Array();
let arrayTwo = [];
{% endhighlight %}

I don't know about you, but I almost always use the second method to declare an array.  In fact, I can't recall a time I've used the first.  But if you like to do it that way, knock yourself out!

Here's an array of cars we'll use in the <code>.forEach()</code> example below:

{% highlight JavaScript %}
let cars = ['BMW', 'Volvo', 'Audi', 'Mercedes', 'Fiat'];
{% endhighlight %}

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Array.forEach()</span>

The <code>.forEach()</code> method can be used in place of the humble <code>for</code> loop.  This method simply loops through each item in the array and leaves it up to you, the developer, to determine what to do with each of those items.  Let's use it to operate on our <code>cars</code> array.

{% highlight JavaScript %}
cars.forEach(function(car) {
  console.log(car);
});
{% endhighlight %}

Here's the result:

{% highlight JavaScript %}
BMW
Volvo
Audi
Mercedes
Fiat
{% endhighlight %}

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Array.map()</span>

The <code>.map()</code> method also loops through the entire array, and returns a <strong>new</strong> array whose contents have been manipulated based upon the return statement(s) that are specified in the return statement of the callback function.

Let's use <code>.map()</code> on an array of numbers.

{% highlight JavaScript %}
let numbers = [2, 4, 6, ,8, 10];
{% endhighlight %}

{% highlight JavaScript %}
let numbersCubed = numbers.map(function(number) {
  return Math.pow(number, 3);
});
{% endhighlight %}

If we run <code>console.log(numbersCubed)</code> this is the result:

{% highlight JavaScript %}
[8, 64, 216, 512, 1000]
{% endhighlight %}

Let's quickly talk about what's going on here.  We declared a new variable, <code>numbersCubed</code>, and set it equal to calling <code>.map()</code> on our original numbers array.  And inside <code>.map()</code> we returned a new array made up of the result of using <code>Math.pow()</code> to cube each of the original numbers.

Side note: If you're not familiar with all of the various methods JavaScript's <code>Math</code> object offers, [check this out](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math).

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Array.filter()</span>

<code>Array.filter()</code> does exactly what it sounds like: it <strong>filters</strong> arrays based on whatever condition we specify in the callback function.  If an array element <strong>does not</strong> pass the condition, it gets filtered out, and the new array that gets returned only includes elements that pass the condition.

Here's another array we'll <code>.filter()</code>:

{% highlight JavaScript %}
let evensAndOdds = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
{% endhighlight %}

Let's filter out the odd numbers and return a new array that only includes even numbers.

{% highlight JavaScript %}
let evensOnly = evensAndOdds.filter(function(number) {
  if (number % 2 == 0) {
    return true;
  } else {
    return false;
  }
});
{% endhighlight %}

What's going on here is pretty simple.  We declare a new array, <code>evensOnly</code> and set it equal to calling <code>.filter()</code> on our original array.  Inside <code>.filter()</code> we use a simple <code>if/else</code> statement to <code>return</code> only the numbers we determine to be even, and thus we end up with a new array that only includes the even numbers from the original array.

This:

{% highlight JavaScript %}
console.log(evensOnly);
{% endhighlight %}

Results in this:

{% highlight JavaScript %}
[2, 4, 6, 8, 10]
{% endhighlight %}

And there you have it: three extremely useful JavaScript array methods.  And those three are just the tip of the iceberg.  There are a ton more that you can read about [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/prototype).

I hope you learned something today that you can use going forward.  Thanks for reading!
