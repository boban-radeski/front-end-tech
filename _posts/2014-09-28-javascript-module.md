---
layout: post
title:  JavaScript module pattern and function prototype
date:   2014-09-28 6:00
tags: module javascript
---

**The module pattern**

In JavaScript variables can belong to global and local scope. Private variable can be achieved with JavaScript closures. 
Global variables can be accessed from all functions. We define global variables using keyword var and name of variable. Keyword var is not required, that mean if we create variable without var it will be always global variable even if is it created inside a function. Global variable belong to window object, they can be changed or used by all scripts in the page. Global variable live as long as application (window/web page) lives.
Example of using global variable:

    var a= 4;
    function myFunction() {
        return a * a;
    }

Local variables is created inside a function and is accessible only in that function scope. It is hidden from other functions and other scripting code. Local variable have short lives. They are created when the function is created, and deleted when the function is finished.
Example of using local variable:

    function myFunction() {
        var a= 4;
        return a * a;
    }


Using global variable in application is not recommended because every function or other code can change or use it, for example if application is developed by two or more developers and they use the same name of global variable. 
The module pattern is popular design that pattern that encapsulates ''privacy", state and organization using closures. According to Douglas Crockford closures are:
"What this means is that an inner function always has access to the vars and parameters of its outer function, even outer function has returned".
In following example we will see module pattern design with closure and self-invoking function.

    var calculator = (function () {
               var x = 0, y = 0; // private variables
               return { // exposed to public
                   add: function (x, y) {
                       return x + y;
                   },
                   minus: function (x, y) {
                       return x - y;
                   },
                   divide: function (x, y) {
                       if (x != 0 && y != 0) {
                           return x / y;
                       }
                   },
                   multiple: function (x, y) {
                       return x * y;
                   }
               }
           }());
           var res = calculator.add(5, 6);
           console.log(res);
           var res1 = calculator.minus(10,4);
           console.log(res1);
           var res2 = calculator.x; // error, x is private and accessible only in calculator function scope


[Live demo](http://jsfiddle.net/13j5wr2y/1/) 

If we call method add from calculator, the output will be sum of two parameters passed in method.
If we try to access variable x or y defined in calculator scope we will see undefined error message.
Module has JSON structure as we can see from above example. Variables can't technically be declared as
public or private in JavaScript unlike some languages(C#, Java, C++) and we 
use function to achieve this concept. With the module pattern, variables or methods declared 
inside the function is visible only in that scope thanks to closures. On the other hand variables 
and methods defined within the returning object are available to everyone.

**Function prototype**

All objects in JavaScript are descended from Object; all objects inherit methods and properties from Object.prototype,
although they may be overridden (except an Object with a null prototype, i.e. Object.create(null)). For example, 
other constructors' prototypes override the constructor property and provide their own toString() methods. Changes to 
the Object prototype object are propagated to all objects unless the properties and methods subject to those changes are
overridden further along the prototype chain. The prototype pattern allows object to inherit from other objects, via their prototypes.
This is an easy and natural way of implementing inheritance in JavaScript. Function prototype works with references. The image bellow visually illustrate  prototypes.

![Alt text](https://haselt.atlassian.net/wiki/download/attachments/14024706/image2014-8-28%2023%3A39%3A57.png?version=1&modificationDate=1409261996432&api=v2 "Optional title")

        var prototypeApp = (function () {
                   var Ford = function () {
                       this.drive = function() {
                           // brm brm f-n
                           console.log("Ford:"+name+" brm brm");
                       };
                   };
                   var Toyota = function () {
                       this.drive = function () {
                           // brm brm f-n
                           console.log("brm brm");
                       };
                   };
                   var Nissan = function () {
                       this.drive = function () {
                           // brm brm f-n
                           console.log("brm brm");
                       };
                   };
                   // usage
                   var ford1 = new Ford();
                   var ford2 = new Ford();
                   var ford3 = new Ford();
                   ford1.drive();
                   ford2.drive();
                   ford3.drive(); // call constructor 3 times, use RAM memory x
                   // With prototype
                   var Car = function () {
                       this.drive = function () {
                           console.log("brm brm with prototype");
                       };
                   };
                   var Ford = function () { };
                   Ford.prototype = new Car();
                   var Toyota = function () { };
                   Toyota.prototype = new Car();
                   var Nissam = function () { };
                   Nissam.prototype = new Car();
                   var ford1 = new Ford();
                   var ford2 = new Ford();
                   var ford3 = new Ford();
                   ford1.drive();
                   ford2.drive();
                   ford3.drive(); // call drive f-n reference 3 times, use RAM memory x/n
               }());

[Live demo](http://jsfiddle.net/13j5wr2y/)
Note: to preview demo use your browser's Console.
The above piece of code shows two different usage of drive() function. In first scenario we have three objects that calls drive() function that is implemented in their constructors, which use x amount of RAM memory. In second scenario with using prototypes drive() function use references that saves a lot of RAM memory. As we can notice one good reason for using prototypes is when we create a lot of copies of objects that share common behaviors.
The main difference between these two scenarios is privacy moment. In first scenario without using prototypes we can access private attributes defined in constructor, for example:


    var Obj = function(){
    var name = "private";
        this.print = function(){
        alert("Prining " + name);
        }
    };
    var obj = new Obj();
    obj.print();

[Live demo](http://jsfiddle.net/kqcchbz7/)