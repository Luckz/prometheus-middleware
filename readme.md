# Node.js simple middleware to expose prometheus metrics

# Purpose

Agent to create an HTTP server to expose prometheus metrics.  
By default it:
- runs an HTTP server to expose metrics
- instantiates and returns a [prom-client](https://www.npmjs.com/package/prom-client)
- patch http server to get request response time
- allows to define custom metrics through prom-client

# Compatibility

Supported and tested : >= 14.0

| Version       | Supported     | Tested         |
|:-------------:|:-------------:|:--------------:|
| 14.x          | yes           | yes            |
| 16.x          | yes           | yes            |

It works with different HTTP server:
- [default Node.js HTTP server](https://nodejs.org/api/http.html#class-httpserver)
- [express](https://expressjs.com/)
- [fastify](https://www.fastify.io/)

# Installation

```console
$ npm install prometheus-middleware --save
```

# Usage

## Basic
```javascript
const APM = require('prometheus-middleware')
const apm = new APM()
apm.init()
```

## Add a custom metric
```javascript
const APM = require('prometheus-middleware')
const apm = new APM()
apm.init()
// ----------------
const counter = new apm.client.Counter({
  name: 'metric_name',
  help: 'metric_help',
})
// ----------------
counter.inc(); // Increment by 1
counter.inc(10); // Increment by 10
```

# Debug

The agent use debug module in order not to pollute your logs.
If you want to see all agent output just use DEBUG environment variable:

```console
DEBUG=prometheus-middleware* node myApp.js
```

# Test

```console
$ npm test
```

Coverage report can be found in coverage/.
