financier
=========

A Node.js module that helps with calculations concerning stocks and portfolios.

## Introduction

Financier is a simple, object-oriented way of managing a portfolio.  This module
was built to calculate the risk in the Bridge Jump Portfolio Management game.

## Installation

    $ npm install financier
```js
var financier = require('financier');
var Stock = financier.Stock;
var Portfolio = financier.Portfolio;
```

## API

### Stock(ticker)

Used to calculate returns and averages for individual stocks.  The parameter
`ticker` determines the stock symbol for the stock.
```js
var AAPL = new Stock('AAPL');
```
