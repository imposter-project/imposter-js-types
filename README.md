# Imposter TypeScript types

- Code autocompletion for your [Imposter](https://github.com/imposter-project/imposter-jvm-engine) JavaScript or TypeScript scripts.
- ES6 and TypeScript support.

## Getting started

The types are published as an [npm package](https://www.npmjs.com/package/@imposter-js/types).

The fastest way to get started is to clone this repository and copy one of the [sample](./samples) projects:

- JavaScript: [imposter-sample-javascript](./samples/imposter-sample-javascript)
- TypeScript: [imposter-sample-typescript](./samples/imposter-sample-typescript)

These samples are preconfigured to transpile and bundle source files down to a single JS file. This can be referenced as the `scriptFile` in your Imposter mock config.

> Note: just update the dependency for `@imposter-js/types` in the `package.json` to the latest from [npmjs.com](https://www.npmjs.com/package/@imposter-js/types)

In the sample project, bundle your script:

    npm run build

In the `dist` directory you will have two files:

```
$ ls
bundle.js
mock-config.yaml
```

This is a valid Imposter configuration - just run `imposter up`

> Install [Imposter CLI](https://github.com/gatehill/imposter-cli) if you don't already have it.

Start your mock:

    $ imposter up
    ...
    Mock server up and running on http://localhost:8080

Hit it:

    $ curl http://localhost:8080
    { "name": "Ada Lovelace" }

The name is dynamically chosen from a list by the script.

Also notice the log output in Imposter:

    DEBUG ... Executed script 'dist/bundle.js' for request: GET http://localhost:8080/ in 6.34ms

## Worked example

This example shows the process in more detail.

Note - this example assumes you know how to set up a bundler/transpiler to emit a single JS file. For a working configuration you can copy see the [sample projects](./samples).

### Prerequisites

- Node.js
- A bundler such as webpack 
- Recommended: Install [Imposter CLI](https://github.com/gatehill/imposter-cli)

### Steps

Add the types to your Node.js module as a dev dependency:

    npm install @imposter-js/types --save-dev

Import the types in your Imposter scripts:

    import {context, logger, respond} from "@imposter-js/types"

Use the objects to write your script, with code autocompletion in your editor/IDE:

```js
logger.info(`Received request: ${context.request}`)

const request = context.request

const body = JSON.stringify({
    "name": "Ada Lovelace",
})

respond()
    .withStatusCode(200)
    .withData(body)
```

Bundle your script:

    npm run build

In the `dist` directory you will have two files:

```
$ ls
bundle.js
mock-config.yaml
```

This is a valid Imposter configuration - just run `imposter up`

> Install [Imposter CLI](https://github.com/gatehill/imposter-cli) if you don't already have it.

Start your mock:

    $ imposter up
    ...
    Mock server up and running on http://localhost:8080

Hit it:

    $ curl http://localhost:8080
    { "name": "Ada Lovelace" }

Also notice the log output in Imposter:

    DEBUG ... Executed script 'dist/bundle.js' for request: GET http://localhost:8080/ in 6.34ms

### Next steps

Because we use a bundler, you can split your scripts across multiple files.

See the `src` directory of the [sample projects](./samples) for an example.

## Related

- [Imposter Mock Engine](https://github.com/imposter-project/imposter-jvm-engine)
- [Imposter JS](https://github.com/imposter-project/imposter-js)