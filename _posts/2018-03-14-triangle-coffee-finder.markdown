---
layout: post
title: "Introducing Triangle Coffee Finder"
permalink: "introducting-triangle-coffee-finder"
date: 2018-03-14
categories: html, css, css gridjavascript, jquery, gulp, sass, web components, polyfills
summary: An introduction to my Triangle Coffee Finder app.
tags: [css, grid, css grid, html, responsive, javascript, jquery, sass, gulp, web components, polyfills]
---

<span style="font-size: 1.25em; font-weight: bold; color: #ac0863;">Today I'm excited to unveil Triangle Coffee Finder!</span>

If you read last week's roundup post, I explained why I hadn't posted a tutorial earlier in the week: I was working on a fun little side project.  Well, today I'm happy to show it off to you!

The premise of Triangle Coffee Finder is simple: answer a few short questions about the type of coffee shop you're looking for in Raleigh, Durham, or Chapel Hill, and get the best possible recommendation in return.  And if the app can't find a perfect match, it will search Yelp! for you.  I think you'll find it's as fun to use as it is simple.

On the surface it doesn't appear overly fancy, but I did incorporate some emerging technology to make it happen.  The application uses  web component specifications for HTML imports and HTML templates.  You can read more about those [here](https://www.webcomponents.org/introduction#html-imports).  Simply put, the application serves up coffee shop recommendations with ease by putting HTML templates inside of other HTML templates on demand.  Because web components are still rather new and haven't been widely adopted, [polyfills](https://www.webcomponents.org/polyfills/) are used to make everything work seamlessly across all web browsers (Right now web components are supported by Chrome and Opera, but not so much by Firefox and Safari).

Other technology used includes vanilla JavaScript, [jQuery](https://www.jquery.com), [Sass](https://www.sass-lang.com), and [Gulp](https://www.gulpjs.com).

Without further delay, here it is...

[Triangle Coffee Finder](https://www.trianglecoffeefinder.com)
