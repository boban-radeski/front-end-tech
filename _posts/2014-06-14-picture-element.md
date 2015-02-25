---
layout: post
title:  Picture Element
date:   2014-08-25 08:00
tags: image responsive picture
---

**Abstract**

This specification defines the HTML picture element and extends the img and source elements to allow authors to declaratively control 
or give hints to the user agent about which image resource to use, based on the screen pixel density, viewport size, image format, and other factors.

**When to use picture**

The picture element is intended to be used when a responsive design dictates a somewhat different image on some types of screens or when providing
 images in multiple file formats.
The picture element is not a general replacement for the img element.
 When there is only a single image source, or when an image source exists in multiple densities, authors are encouraged to use just the img element, rather than cluttering their page with additional unnecessary syntax.
<br />
Example:

    <!DOCTYPE html>
    <html>
    <head>
    <title>We are ready part 1</title> 
        <style>
            img{
                max-width:100%;
            }
        </style>
    </head>
    <body>
    <h1> The picture element </h1>
    <picture>
        <source media="(max-width: 600px)" srcset="small.png">
        <source media="(min-width: 601px)" srcset="large.jpg">
        <img src="logo.png" alt="HASLET image" />
    </picture>
    </body>
    </html>

**Result**

*  **Case 1: Set browser to size smaller than 600px**

![demo image](/front-end-tech/assets/images/small-prtsc.png)

* **Case 2: Set browser size greater than 601px**

![demo image](/front-end-tech/assets/images/large-prtsc.png)
