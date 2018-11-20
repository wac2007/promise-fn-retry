# Promise Retry
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/felippemauricio/promise-fn-retry/blob/master/LICENSE)
[![npm version](https://img.shields.io/npm/v/promise-fn-retry.svg?style=flat)](https://www.npmjs.com/package/promise-fn-retry)
[![Build Status](https://travis-ci.org/felippemauricio/promise-fn-retry.svg?branch=master)](https://travis-ci.org/felippemauricio/promise-fn-retry)
[![devDependencies Status](https://david-dm.org/felippemauricio/promise-fn-retry/dev-status.svg)](https://david-dm.org/felippemauricio/promise-fn-retry?type=dev)
[![Coverage Status](https://coveralls.io/repos/github/felippemauricio/promise-fn-retry/badge.svg?branch=master)](https://coveralls.io/github/felippemauricio/promise-fn-retry?branch=master)
[![Code Style](https://badgen.net/badge/code%20style/airbnb/fd5c63)](https://github.com/airbnb/javascript)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/felippemauricio/promise-fn-retry/pulls)

Abstraction for exponential and custom retry strategies to failed promises. Retrying made simple and easy. \o/

## Installation

Using yarn:
```js
yarn add promise-fn-retry
```

Using npm:

```js
npm i --save promise-fn-retry
```

## Usage

```js
  import fetch from 'node-fetch';
  import retry from 'promise-fn-retry';

  const requestUser = () => {
    // Create a function that return a promise
    const promiseFn = () => fetch('https://api.github.com/users/14');

    // call retry passing as an argument the promiseFn. Thats it!
    return retry(promiseFn)
      .then(res => res.json());
  };

  export default requestUser;

```

```js
  import fetch from 'node-fetch';
  import retry from 'promise-fn-retry';

  const requestUser = () => {
    // Create a function that return a promise
    const promiseFn = () => fetch('https://api.github.com/users/14');

    // You can use options to your retry rules strategy.
    const options = {
      times: 3,
      initialDelay: 100,
    };

    // call retry passing as an argument the promiseFn. Thats it!
    return retry(promiseFn, options)
      .then(res => res.json());
  };

  export default requestUser;

```

## API

```js
  retry(promiseFn : Function, options : Object) => Promise
```

### Options

| OPTION                                     | DEFAULT                | DESCRIPTION                                                   |
|--------------------------------------------|:----------------------:|---------------------------------------------------------------|
| times                                      | 1                      | Retry Times (Number)                                          |
| initialDelayTime                           | 100                    | Delay to start new retry (Number)                             |
| onRetry                                    |                        | Function that is called after retry (Function). ex: metrics   |
| shouldRetry                                |                        | Function called after retry (Function). ex: auth error        |

