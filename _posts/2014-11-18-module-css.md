---
layout: post
title:  Module CSS using LESS pre-processor
date:   2014-11-18 9:00
tags: module less css 
---

**Intoduction**

Module CSS is one part of SMACSS or Scalable and Modular CSS and its main goal is to keep elements independent so they can exist 'alone'. Shortly let's say we have navigation menu as module and we want to reuse it in other project(s). We should only copy and paste required files in new project and menu should work and look same as in previous project. 
Let's see below piece of code:
Let's see below piece of cake code:

   *   Bad example

    <ul class="nav-menu-wrapper">
        <li>
            <a href="#">HOME</a>
        </li>
        .....
    </ul>

and then in CSS:

    ul.nav-menu-wrapper{ /* style of menu list */}
	    ul.nav-menu-wrapper li { /* style of list item */}
	    ul.nav-menu-wrapper li a { ... }
	
	or more badly in CSS pre-processors(LESS, SASS):
	ul.nav-menu-wrapper{
		li{
			a{
			   //evil nesting, don't try it at home
			}
		}
	}


If above code we save it in .html and .css files it will work correctly. But what if in the future or in next project we want or have request to replace all a hrefs with buttons, or all list items with div elements. In that situation we need to change both html and css files which is not correct solution.
With Module CSS we solve this kind of issue by attaching classes to each single element as below:

   *  Good Example

If above code we save it in .html and .css files it will work correctly. But what if in the future or in next project we want or have request to replace all a hrefs with buttons, or all list items with div elements. In that situation we need to change both html and css files which is not correct solution.
With Module CSS we solve this kind of issue by attaching classes to each single element as below:

    <ul class="hs-nav-menu-wrapper">
	    <li class="hs-nav-menu-item">
		    <a href="#" class="hs-nav-menu-link">Home</a>
	    </li>
	    <li class="nav-menu-item">
		    <a href="#" class="nav-menu-link">Home</a>
	    </li>
	    <li class="nav-menu-item">
		    <a href="#" class="nav-menu-link">Home</a>
	    </li>
     </ul>

and then in CSS:

    .hs-nav-menu-wrapper .hs-nav-menu-item { .... }
     .hs-nav-menu-wrapper .hs-nav-menu-link { .... }
 
     or in LESS/SASS
     .hs-nav-menu-wrapper{
	    .hs-nav-menu-item { ... }
	    .hs-nav-menu-link { ... }
     }

Note: as you can see we add prefix "hs"(what mean HASELT) to classes as stamp of our property.

For further reading about SMACSS: https://smacss.com/
Any questions or discussion are more than welcome (smile)