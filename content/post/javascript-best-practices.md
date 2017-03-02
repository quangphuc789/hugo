+++
date = "2017-01-11T09:02:12+08:00"
title = "Javascript Best Practices"
draft = false
tags = ['javascript', 'best-practices']
categories = ["Software Engineering"]

+++

![image](https://i.stack.imgur.com/Mmww2.png)

*Avoid Global Variables*

Minimize the use of global variables.

This includes all data types, objects, and functions.

Global variables and functions can be overwritten by other scripts.

Use local variables instead, and learn how to use closures.

*Always Declare Local Variables*

All variables used in a function should be declared as local variables.

Local variables must be declared with the var keyword, otherwise they will become global variables.

`Strict mode` does not allow undeclared variables.

*Declarations on Top*

It is a good coding practice to put all declarations at the top of each script or function.

This will:

Give cleaner code

Provide a single place to look for local variables

Make it easier to avoid unwanted (implied) global variables

Reduce the possibility of unwanted re-declarations

```
// Declare at the beginning
var firstName, lastName, price, discount, fullPrice;

// Use later
firstName = "John";
lastName = "Doe";

price = 19.90;
discount = 0.10;

fullPrice = price * 100 / discount;
```

This also goes for loop variables:

```
// Declare at the beginning
var i;

// Use later
for (i = 0; i < 5; i++) {
```