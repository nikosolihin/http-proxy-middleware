# Proxy Events

Subscribe to [`http-proxy`](https://github.com/nodejitsu/node-http-proxy) [![GitHub stars](https://img.shields.io/github/stars/nodejitsu/node-http-proxy.svg?style=social&label=Star)](https://github.com/nodejitsu/node-http-proxy) events: `error`, `proxyReq`, `proxyReqWs`, `proxyRes`, `open`, `close`.

## onError

Subscribe to http-proxy's [error event](https://www.npmjs.com/package/http-proxy#listening-for-proxy-events).

```javascript
const { createProxyMiddleware } = require('http-proxy-middleware');

const onError = function (err, req, res) {
  console.log('Something went wrong.');
  console.log('And we are reporting a custom error message.');
};

const options = { target: 'http://localhost:3000', onError: onError };

const apiProxy = createProxyMiddleware('/api', options);
```

## onProxyReq

Subscribe to http-proxy's [proxyReq event](https://www.npmjs.com/package/http-proxy#listening-for-proxy-events).

```javascript
const { createProxyMiddleware } = require('http-proxy-middleware');

const onProxyReq = function (proxyReq, req, res) {
  // add new header to request
  proxyReq.setHeader('x-added', 'foobar');
};

const options = { target: 'http://localhost:3000', onProxyReq: onProxyReq };

const apiProxy = createProxyMiddleware('/api', options);
```

## onProxyReqWs

Subscribe to http-proxy's [proxyReqWs event](https://www.npmjs.com/package/http-proxy#listening-for-proxy-events).

```javascript
const { createProxyMiddleware } = require('http-proxy-middleware');

const onProxyReqWs = function (proxyReq, req, socket, options, head) {
  // add custom header
  proxyReq.setHeader('X-Special-Proxy-Header', 'foobar');
};

const options = { target: 'http://localhost:3000', onProxyReqWs: onProxyReqWs };

const apiProxy = createProxyMiddleware('/api', options);
```

## onProxyRes

Subscribe to http-proxy's [proxyRes event](https://www.npmjs.com/package/http-proxy#listening-for-proxy-events).

```javascript
const { createProxyMiddleware } = require('http-proxy-middleware');

const onProxyRes = function (proxyRes, req, res) {
  // add new header to response
  proxyRes.headers['x-added'] = 'foobar';

  // remove header from response
  delete proxyRes.headers['x-removed'];
};

const options = { target: 'http://localhost:3000', onProxyRes: onProxyRes };

const apiProxy = createProxyMiddleware('/api', options);
```
