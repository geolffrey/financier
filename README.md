financier
=========

A Node.js module that helps with calculations concerning stocks and portfolios.

## Introduction

Financier is a simple, object-oriented way of managing a portfolio.  This module
was built to calculate the risk in the Bridge Jump Portfolio Management game.

## Installation

`$ npm install financier`

```js
var financier = require('financier');
var Stock = financier.Stock;
var Portfolio = financier.Portfolio;
```

## API

### Stock(_String_ ticker)

Used to calculate returns and averages for individual stocks.  The parameter
`ticker` determines the stock symbol for the stock.

```js
var AAPL = new Stock('AAPL');
```
#### Properties

  *__ticker__ - `String` The stock symbol.
  *__returns__ - `Array` The array of tick returns for the stock.
  *__average__ - `Float` The average of all the tick returns.

#### Stock.push(_Float_ open, _Float_ close, _Boolean_ _(Opt)_ wait)
Add a tick of data to the stock history.  This new return is stored in the
`returns` property for the stock.  Default behaviour immediately recalculates
the overall average on returns.

If `wait` is `true`, the average is not calculated.

```js
// Push a return of 5.8 to the list of returns.  The overall average return will
// be automagically calculated.
AAPL.push(106.5, 112.3);
```
