# crawler

> Web crawler based on [`Puppeteer`](https://github.com/GoogleChrome/puppeteer)

[![node (scoped)](https://img.shields.io/node/v/@opd/crawler.svg)](https://www.npmjs.com/package/@opd/crawler)
[![npm (scoped)](https://img.shields.io/npm/v/@opd/crawler.svg)](https://www.npmjs.com/package/@opd/crawler)
![build](https://github.com/open-data-plan/crawler/workflows/build/badge.svg)
[![Build Status](https://dev.azure.com/kagawagao/OPD/_apis/build/status/open-data-plan.crawler?branchName=master)](https://dev.azure.com/kagawagao/OPD/_build/latest?definitionId=3&branchName=master)
[![Coverage Status](https://coveralls.io/repos/github/open-data-plan/crawler/badge.svg?branch=master)](https://coveralls.io/github/open-data-plan/crawler?branch=master)

## Install

```bash
npm install @opd/crawler
```

## Use

```js
import Crawler from '@opd/crawler'
// or commonjs
const Crawler = require('@opd/crawler').default

const crawler = new Crawler(options)
```

## API

### `new Crawler(options)`

create crawler instance

`options`: crawler instance config

- `parallel`: maximum number of crawlers, default is `5`
- `pageEvaluate`: evaluate function on current page, see [`Puppeteer`](https://pptr.dev/#?product=Puppeteer&version=v1.18.1&show=api-pageevaluatepagefunction-args), **cannot support extra args now**

### `crawler.launch([options])`

launch browser use [`puppeteer.launch`](https://pptr.dev/#?product=Puppeteer&version=v1.18.1&show=api-puppeteerlaunchoptions)

### `crawler.queue(urls)`

add urls to crawler queue

> Note: check url **strictly**, means url must start with `https?`

### `crawler.start([urls]): PageResult[]`

start crawl page, if `urls` is presented, will call `crawler.queue` firstly.

```js
const result = await crawler.start()
console.log(result)

// [
//   {
//     url, // page url
//     result // crawled result
//   }
// ]
```

> Note: if you call `start` before `launch`, `browser` will also be launched, but with no extra launch options
