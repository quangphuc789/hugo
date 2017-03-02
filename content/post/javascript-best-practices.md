+++
date = "2017-01-11T09:02:12+08:00"
title = "Javascript Best Practices"
draft = false
tags = ['javascript', 'best-practices']
categories = ["Software Engineering"]

+++

All these practices are within my personal knowledge & experience, with references at the bottom of the page.

![image](https://i.stack.imgur.com/Mmww2.png)

***1. Don't mess with === and ==***

The **==** comparison operator always converts (to matching types) before comparison. Similar concept in PHP programming. It is a loose comparison. Don't use it unless you know what it does. Seasoned Javascript developers do feel very 'itchy' if they see the usage of '==' for no good reason.

The **===** compares both values and type. This is a strict comparison, like in other strong type language, such as Java or C++.

Some examples:

```
0 == "";        // true
1 == "1";       // true
1 == true;      // true

0 === "";       // false
1 === "1";      // false
1 === true;     // false
```

***2. Don't forget to initialise***

When writing a function, in other languages, developers can easily assign default values to the parameters within the function definition itself. This greatly reduces the chance of crashing the program due undefined data. For example, in PHP:

```
function getSomeInfo($docID, $reference = 2) {
    // In this function, only $docID is needed
    $document = Document::model()->getDocFromId($docID, $reference);
}
```

In Javascript, there is no obvious way, developers are to check themselves. But this should not stop us from building a good habit of initialising values.

```
function getSomeInfo(docId, reference) {
    if (reference === undefined) {
        reference = 0;
    }
}
```

Always declare variables first, and on top of the function, tell clearly what they are doing. Then initialise them.

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

***3. Use English, pronounceable, and meaningful identity names***

Except the loop iterator indexes.

```
var xxyyzz = '15';          // Bad
var taklabukab3 = 4         // Bad
var thisIsAnotherVar = 9    // Bad

var todayDate = new Date(); // Good
var employeeSalary = 500;   // Good
var studentNameLists = [];  // Good
```

***4. End Your Switches with Defaults. And use Breaks***

End the switch with default keyword, and know how to use or not to use breaks.

```
switch (new Date().getDay()) {
    case 0:
        day = "Sunday";
        break;
    case 1:
        day = "Monday";
        break;
    case 2:
        day = "Tuesday";
        break;
    case 3:
        day = "Wednesday";
        break;
    case 4:
        day = "Thursday";
        break;
    case 5:
        day = "Friday";
        break;
    case 6:
        day = "Saturday";
        break;
    default:
        day = "Unknown";
}
```


*References*

[W3Schools](https://www.w3schools.com/js/js_best_practices.asp) | [DevBridge](https://www.devbridge.com/articles/javascript-best-practices/) | [Clean Code Javascript](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)