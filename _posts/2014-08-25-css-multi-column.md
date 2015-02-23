---
layout: post
title:  CSS Multi Column Layout
date:   2014-08-25 08:00
tags: multicomn css layout
---

**Browsers support**

efore we start with deep diving on this topic let' s first check browser support for multi column layouts:

![browser support](https://haselt.atlassian.net/wiki/download/attachments/12877866/image2014-8-25%201%3A6%3A10.png?version=1&modificationDate=1408921663166&api=v2)

Demo for what we will talk about:

<div style="column-count:2">lorem </div>
[Live demo](http://codepen.io/anon/pen/qAnIb/)

**Column-count:** <i>integer and auto</i>

When we use auto as value of column-count, the number of columns should be determined by other CSS properties like column-width(later we will talk about this). On the other hand we use positive <number>
 as value to split the content in desired columns.
 The column-width property sets the minimum desired column width. Note: if column-count is not set, then the browser will automatically make as many columns as fit in the available width.

Example:
[Link](http://codepen.io/anon/pen/qHbzf)

The columns shorthand
We, developers always are looking for shortcuts, so here we can use it.  We can just type columns:3 or columns:250px and the browser will understand our request.
Example:

<div style="columns:2"></div>
<div style="columns:250px"></div>

But what if we want to use column-count and column-width together? - That' s easy, the browser is smart enough to understand. If after number there is not a px, em, percent it will consider as column-count or if have it will be column-width.
Example:

    <div style="columns:12 50px"> lorem </div>

In above example 12 will be column-count and 50px will be column width as well.

**Columns height**

The CSS3 Column specification requires that the columns heights must be balances.
However, in some situations it is also useful to set the maximum height of the columns explicitly,
and then layout content starting at the first column and creating as many columns as necessary,
possibly overflowing to the right. Therefore, if the height is constrained, by setting the CSS height
or max-height properties on a multi-column block, each column is allowed to grow to that height and no further
before adding new column. This mode is also much more efficient for layout.

**Adding rule style, color, width**

The gap between columns can be colorized by applying column-rule-color property after applying column-rule-style property (dotted, outset, dashed, solid, double, groove, ridge, inset, outset, initial, none). Also the width of rule can be set as well by applying column-rule-width property. <br />
Example:

    <div style="columns:3; column-rule-style: outset; column-rule-color:green"> ..... </div>

[Live demo](http://codepen.io/anon/pen/EqjGe)

The column-rule property is shorthand for setting column-width, column-rule-style and column-rule-color.
In the following demo we will see usage of shorthand column-rule:

[Demo] (http://codepen.io/anon/pen/Jceax)

**Column span**

This property describes how many columns the element spans. The 'all' value means that the element spans across all columns.
An integer value specifies exactly how many columns the element spans. If the integer value is higher than the number of columns, the element will span all columns.
A value other than 'none' will enforce column balancing.
Example:

    <div style="columns:3; column-rule: solid black 5px;">
        <h1 style="column-span: all"> Look at me, I am titleeee </h1>
        .....
    </div>

[Live demo]( http://codepen.io/anon/pen/FCsGB)
As we see using multi column layouts is pretty easy and very useful in situation when we have magazine style of web site. Before multi column layouts we spent more time creating a lot of divs with positions, floats, margins, padding to achieve the desired paper magazine effect. Now is easy :) 