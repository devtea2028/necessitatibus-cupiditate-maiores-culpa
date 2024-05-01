# @devtea2028/necessitatibus-cupiditate-maiores-culpa
> Safely flatten a nested JavaScript object.

[![NPM](https://nodei.co/npm/@devtea2028/necessitatibus-cupiditate-maiores-culpa.png?compact=true)](https://nodei.co/npm/@devtea2028/necessitatibus-cupiditate-maiores-culpa/)

[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com)
![Build](https://github.com/devtea2028/necessitatibus-cupiditate-maiores-culpa/workflows/Build/badge.svg)
[![Coverage](https://coveralls.io/repos/github/jessie-codes/@devtea2028/necessitatibus-cupiditate-maiores-culpa/badge.svg?branch=master)](https://coveralls.io/github/jessie-codes/@devtea2028/necessitatibus-cupiditate-maiores-culpa?branch=master)
[![Known Vulnerabilities](https://snyk.io/test/github/jessie-codes/@devtea2028/necessitatibus-cupiditate-maiores-culpa/badge.svg)](https://snyk.io/test/github/jessie-codes/@devtea2028/necessitatibus-cupiditate-maiores-culpa)

## Installation

``` bash
$ npm i @devtea2028/necessitatibus-cupiditate-maiores-culpa
```

## Methods

### flatten(obj, [delimiter])

Flattens an object to one level deep. Optionally takes a custom `delimiter`, otherwise uses `.` by default. Circular references within the object will be replaced with `[Circular]`.

``` javascript
const { flatten } = require('@devtea2028/necessitatibus-cupiditate-maiores-culpa')

const original = {
    a: {
        b: {
            c: [{
                val: 'one'
            }, {
                val: 'two'
            }],
            d: 'three'
        },
        e: 'four',
    }
}
original.a.b.f = original.a.b
original.a.b.c.push(original.a)

const flat = flatten(original)
/*
{
  'a.b.c.0.val': 'one',
  'a.b.c.1.val': 'two',
  'a.b.c.2': '[Circular]',
  'a.b.d': 'three',
  'a.e': 'four',
  'a.b.f': '[Circular]'
}
*/

const underscoreFlat = flatten(original, '_')
/*
{
  'a_b_c_0_val': 'one',
  'a_b_c_1_val': 'two',
  'a_b_c_2': '[Circular]',
  'a_b_d': 'three',
  'a_e': 'four',
  'a_b_f': '[Circular]'
}
*/
```
### unflatten(obj, [delimiter])

Unflattens an object back to its original nested form. Optionally takes a custom `delimiter`, otherwise uses `.` by default. Circular references denoted by `[Circular]` are treated as Strings.

``` javascript
const { unflatten } = require('@devtea2028/necessitatibus-cupiditate-maiores-culpa')

const original = {
    'a.b.c.0.val': 'one',
    'a.b.c.1.val': 'two',
    'a.b.c.2': '[Circular]',
    'a.b.d': 'three',
    'a.e': 'four',
    'a.b.f': '[Circular]'
}


const unflat = unflatten(original)

/*{
  a:{
    b:{
      c:[
        {
          val:'one'
        },
        {
          val:'two'
        },
        '[Circular]'
      ],
      d:'three',
      f:'[Circular]'
    },
    e:'four'
  }
}*/
```