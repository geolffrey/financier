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

* __ticker__ - `String` The stock symbol.
* __returns__ - `Array` The array of tick returns for the stock.
* __average__ - `Float` The average of all the tick returns.

#### Stock.push(_Float_ open, _Float_ close, _Boolean_ _[Opt]_ wait)
Add a tick of data to the stock history.  This new return is stored in the
`returns` property for the stock.  Default behaviour immediately recalculates
the overall average on returns.

The parameters `open` and `close` are `floats` representing the price of the stock.
If `wait` is `true`, the average is not calculated.

```js
// Push a return of 5.8 to the list of returns.  The overall average return will
// be automagically calculated.
AAPL.push(106.5, 112.3);
```

#### _Float_ Stock.calculateAverage()
Calculate the average of all the returns.  This new average is both returned and
stored in the `average` property for the stock.

It is only necesarry to call this function if you are adding returns in bulk.

```js
function randomValue() {
    return 100 + Math.random() * 30;
}

// Simulate adding thousands of returns to a stock.
for (var i = 0; i < 10000; i++) {
    // Push the data, but hold off on calculating the average.
    AAPL.push(randomValue(), randomValue(), true);
}

// Now calculate the overall average.
AAPL.calculateAverage();
```

### Portfolio()

Keeps data on a portfolio, and has methods to calculate its attributes.

```js
var clientPortfolio = new Portfolio();
```

#### Properties

* __stocks__ - `Object` Stocks included in the portfolio.
* __value__ - `Float` Total market value for the stock.
* __risk__ - `Flat` Risk for the entire portfolio.
* __cache__ - `Cache` Cache of portfolio securities.

#### Portfolio.addStock(_Stock_ stock, _Float_ value, _Boolean_ _[Opt]_ clone)
Add a stock to the portfolio.  This stock is stored in the `stocks` property
for the portfolio.  Relative weights for the entire portfolio are automagically
recalculated.

The parameter `stock` is the `Stock` object being added.  `value` represents the
market value for the security as a `float`.  Currency should be kept consistent.
If `clone` is `true`, a new `Stock` is created with identical `ticker`, `return`,
and `average` properties.

__IMPORTANT:__ If stocks are reused in multiple portfolios, or need to be kept
independent of the portfolio, they _MUST_ be cloned to prevent discrepencies with
how JavaScript passes objects by reference.

```js
// Add AAPL to multiple client portfolios:
clientPortfolio.addStock(AAPL, 100323.33, true);
otherClientPortfolio.addStock(AAPL, 1483.63, true);

var open = 135.3;
var close = 123.53;

// If new return history needs to be added, it must be done individually.
AAPL.push(open, close);
clientPortfolio.stocks.AAPL.push(open, close);
otherClientPortfolio.stocks.AAPL.push(open, close);
```
