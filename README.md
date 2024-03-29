# Grain Web Example

This repo contains an example of Grain wasm files running in a browser.

## Setup

First, you'll need to install the Grain compiler by following the [Getting Grain](https://grain-lang.org/docs/getting_grain) guide for your operating system.

Additionally, you'll need to install the project dependencies using:

```sh
npm install
```

The easiest way to compile your Grain files to WebAssembly is to use the built-in npm script:

```sh
npm run compile
```

This will compile `hello.gr`, `another.gr`, and the necessary stdlib dependencies.

Then, run a webserver in this directory. You can use our other npm script:

```sh
npm start
```

(This script will also compile your project before starting the webserver).

If you visit `localhost:1337` and open your dev console, you should see the hello world messages appear.

## `index.html` Breakdown

We first load the Grain browser runtime with this script tag:

```html
<script src="node_modules/@grain/js-runner/dist/grain-runner-browser.js"></script>
```

`Grain.buildGrainRunner` takes a locator function as its argument. In this case, we just use the `defaultURLLocator`. As arguments, we pass the locations to look for wasm files—the current URL as the root, and the `node_modules/@grain/stdlib` subdirectory. The default locator will try to find wasm files by first looking in the root of this project, followed by the stdlib directory.

Once the `GrainRunner` is set up, we call `GrainRunner.runURL` with `hello.wasm`. The locator will then fetch `hello.wasm`, see that it depends on `another.wasm` and `pervasives.wasm`, and load those as well.
