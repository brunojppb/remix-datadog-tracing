# Remix Express Starter

This repo is a Remix project that reproduces an issue with the
[dd-trace](https://github.com/DataDog/dd-trace-js) library version **4.8.1**
where routes handled by Remix using Express in a catch-all route handler are
generating resources named with `GET` only in the APM UI.

Here is how the Datadog UI looks like:

## How to reproduce the issue

First install all dependencies with:

```shell
npm install
```

Then, build the app with:

```sh
NODE_ENV=production npm run build
```

Then run the app in production mode enabling the Datadog tracer:

```sh

NODE_ENV=production \
  DD_TRACE_ENABLED=true \
  DD_TRACE_DEBUG=true \
  DD_SERVICE=remix-demo \
  PORT=3000 \
  node --require dd-trace/init ./build/index.js

```

## Docker

This demo includes a Dockerfile which builds a production-ready Docker image
also with dd-trace enabled. Just go ahead and build it:

```shell
docker build .
```

upon running the container, assuming there is a datadog agent available, traces
should start to come in the APM.

### DIY

If you're familiar with deploying express applications you should be right at
home just make sure to deploy the output of `remix build`

- `build/`
- `public/build/`