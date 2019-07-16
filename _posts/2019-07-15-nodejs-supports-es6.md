---
layout: post
title:  "Node.js 12 supports ES6, Difference b/w Vanilla Js and ES2015+"
date:   2019-05-23 21:03:36 +0530
---
If you are a Node.js developer either by writing Node.js apps or libraries, you probably know that Node.js 12 supports ECMAScript standard modules. This feature will probably be stable by October 2019.

### **Do you know what are the differences between VannilaJS and ES modules?**

## Variable Declaration (let and const)
* **let** and **const** are blocked scoped
* **var** are function scoped

```js
    // ES5
    var name5 = 'Jane Smith';
    var age5 = 23;
    name5 = 'Jane Miller';
    console.log(name5);

    // ES6
    const name6 = 'Jane Smith';
    let age6 = 23;
    name6 = 'Jane Miller';
    console.log(name6);
```

### Blocks and IIFEs
```js
    // ES6
    {
        const a = 1;
        let b = 2;
        var c = 3;
    }

    console.log(a + b); //throws error because let and const are blocked scoped
    console.log(c); //returns 3 because var is function scoped

    // ES5
    (function() {
        var c = 3;
    })();
    console.log(c); //throws error because var is function scoped
```

## Strings in ES6
We can use backticks to append strings and variables
```js
    let firstName = 'John';
    let lastName = 'Smith';
    const yearOfBirth = 1990;
    function calcAge(year) {
        return 2016 - year;
    }

    // ES5
    console.log('This is ' + firstName + ' ' + lastName + '. He was born in ' + yearOfBirth + '. Today, he is ' + calcAge(yearOfBirth) + ' years old.');

    // ES6
    console.log(`This is ${firstName} ${lastName}. He was born in ${yearOfBirth}. Today, he is ${calcAge(yearOfBirth)} years old.`);
```

## Arrow Functions
```js
    const years = [1990, 1965, 1982, 1937];

    // ES5
    var ages5 = years.map(function(el) {
        return 2016 - el;
    });
    console.log(ages5);
    //returns [26, 51, 34, 79]

    // ES6
    let ages6 = years.map(el => 2016 - el);
    console.log(ages6);
    //returns [26, 51, 34, 79]
```

## Arrays in ES6
```js
    //ES5
    var ages = [12, 17, 8, 21, 14, 11];
    var full = ages.map(function(cur) {
        return cur >= 18;
    });
    console.log(full);
    console.log(full.indexOf(true));
    console.log(ages[full.indexOf(true)]);

    //ES6
    console.log(ages.findIndex(cur => cur >= 18));
    console.log(ages.find(cur => cur >= 18));
```

## Spread Operator ES6
```js
    function addFourAges (a, b, c, d) {
        return a + b + c + d;
    }

    var sum1 = addFourAges(18, 30, 12, 21);
    console.log(sum1);

    //ES5
    var ages = [18, 30, 12, 21];
    var sum2 = addFourAges.apply(null, ages);
    console.log(sum2);

    //ES6
    const sum3 = addFourAges(...ages);
    console.log(sum3);

    const familySmith = ['John', 'Jane', 'Mark'];
    const familyMiller = ['Mary', 'Bob', 'Ann'];
    const bigFamily = [...familySmith, 'Lily', ...familyMiller];
    console.log(bigFamily);
```

## Rest Parameter
Rest parameter are iterating unlimited parameters from a function
```js
    //ES5
    function isFullAge5() {
        //console.log(arguments);
        var argsArr = Array.prototype.slice.call(arguments);
        
        argsArr.forEach(function(cur) {
            console.log((2016 - cur) >= 18);
        })
    }
    isFullAge5(1990, 1999, 1965);
    isFullAge5(1990, 1999, 1965, 2016, 1987);


    //ES6
    function isFullAge6(...years) {
        years.forEach(cur => console.log( (2016 - cur) >= 18));
    }

    isFullAge6(1990, 1999, 1965, 2016, 1987);
```

## Default Parameter
```js
    function SmithPerson(firstName, yearOfBirth, lastName, nationality) {
        
        lastName === undefined ? lastName = 'Smith' : lastName = lastName;
        nationality === undefined ? nationality = 'american' : nationality = nationality;
        
        this.firstName = firstName;
        this.lastName = lastName;
        this.yearOfBirth = yearOfBirth;
        this.nationality = nationality;
    }


    //ES6
    function SmithPerson(firstName, yearOfBirth, lastName = 'Smith', nationality = 'american') {
        this.firstName = firstName;
        this.lastName = lastName;
        this.yearOfBirth = yearOfBirth;
        this.nationality = nationality;
    }


    var john = new SmithPerson('John', 1990);
    var emily = new SmithPerson('Emily', 1983, 'Diaz', 'spanish');
```

## Import and Export
Normally import and export in Vanilla Js would be require and module.export as follow
```js
    //Export
    //helloWorld.js
    module.exports = 'Hello World';

    //Import
    const str = require('./helloWorld');
    console.log(str);
```

ES6 Syntax as follow
```js
    //Export
    //helloWorld.js
    export default {
        const str = 'Hello World';
    }

    //Import
    import { str } from './helloWorld';
    console.log(str);
```

## That's it
Thanks for reading! Happy Coding :).