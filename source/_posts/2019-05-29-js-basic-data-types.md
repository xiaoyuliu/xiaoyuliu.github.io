
---
title: JavaScript Basic Data Types
date: Wed May 29 09:10:36 2019
categories: Web Developer Bootcamp
tag:
- front end
- javascript
---

### Number

#### Special Numbers

1. `Number.MAX_VALUE` : the maximum positive integer number supported in JS
2. `Number.MIN_VALUE` : the minimum positive number supported in JS
3. `NaN` : not a number, but still `number` type
4. `Infinity` : positive infinity
5. `-Infinity` : negative infinity

All special numbers will still return `number` when used `typeof X`

#### Calculation

JavaScript can support accurate integer manipulations, but not float numbers.

### String

Nothing special

### Boolean

Nothing special

### Undefined

Only declaration, no definition.
`typeof undefined = undefined`

### Null

`typeof null = object`

### Convert to String

- Use `var str = XXX.toString()` except `null` and `undefined`
- Use `String(XXX)` include `null` and `undefined`

### Convert to Number

- Use `Number()`:
    + For String
        * if only contain numbers, convert to number
        * if not empty string and not only number, convert to `NaN`
        * if empty string or all spaces, convert to `0`
    + For Boolean
        * true -> `1`
        * false -> `0`
    + For Null
        * `0`
    + For Undefined
        * `NaN`

- Use `parseInt()` and `parseFloat` only for String:
    + If string contains any number, convert the starting number part only
    + E.g. 123px -> 123
    + If string doesn't start with number, convert to `NaN`
    + `parseFloat` works similarly with `parseInt`
    + If apply these two methods for un-strings, the method will convert the object to a string first then apply. Therefore for `boolean`, always get `NaN`

#### Different scales

- Numbers in hexadecimal(16) start with `0x`
- Numbers in octonary(8) start with `0`
- Nunbers in binary start with `0b` (not supported by all browsers)
- For strings start with `0`, some browsers will interpret as octonary and others treat as decimalism. So use `parseInt(XXX, 10/16/8/2)` to indicate the scale.

### Conver to Boolean

Only one way to use `Number(XXX)`

1. For Number, only `0` and `NaN` will be converted to `false`.
2. For String, only empty string will give `false`
3. `null` and `undefined` will give `false`
4. `object` will give `true` 

### Manipulation of basic data types

1. Anything `+` a string will be converted to string first. 
    
    E.g. 1 + "abc" = "1abc"

2. Others will be converted to number first.
    
    E.g. "123" - 0 = 123

3. Using `+` can convert other data types into `Number`

    E.g. +"123" = 123

4. The result of comparison between `NaN` and any data is `false`. Even using `b == NaN` will always return `false`, we need to use `isNaN(b)`
5. If two strings are compared, using their unicodes to compare bit by bit
6. Use `===` and `!==` to compare two data considering data types at the same time

### Unicode

1. Use Unicode in strings: "/uXXXX"
2. Use Unicode in web: &#XXXX; (decimalism)



