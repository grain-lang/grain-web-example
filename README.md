# Grain Web Example

This repo contains an example of Grain wasm files running in a browser.

## Setup

You'll first need to compile the wasm files. The easiest way to do this is to use the Grain cli:

```sh
grain hello.gr --stdlib=./stdlib
```

This will compile `hello.gr`, `another.gr`, and the necessary stdlib dependencies. Note that I copied Grain's standard library into this project—in the future, the standard library will be available as a consumable package from npm.

Run a webserver in this directory. If you have Python 3 on your computer, you can run

```sh
python -m http.server
```

If you visit `localhost:8000` and open your dev console, you should see the hello world messages appear.

## `index.html` Breakdown

We first load the Grain browser runtime with this script tag:

```html
<script src="js/grain-runtime-browser.js"></script>
```

`Grain.buildGrainRunner` takes a locator function as its argument. In this case, we just use the `defaultURLLocator`. As arguments, we pass the locations to look for wasm files—the current URL as the root, and the `stdlib` subdirectory. The default locator will try to find wasm files by first looking in the root of this project, followed by the stdlib directory.

Once the `GrainRunner` is set up, we call `GrainRunner.runURL` with `hello.wasm`. The locator will then fetch `hello.wasm`, see that it depends on `another.wasm` and `pervasives.wasm`, and load those as well.
