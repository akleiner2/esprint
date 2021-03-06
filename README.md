# esprint [![Build Status](https://img.shields.io/travis/arthuralee/esprint/master.svg?style=flat)](https://travis-ci.org/arthuralee/esprint) [![npm version](https://img.shields.io/npm/v/esprint.svg?style=flat)](https://www.npmjs.com/package/esprint)

esprint speeds up eslint by running the linting engine across multiple threads, and optionally sets up a server daemon to cache the lint status of each file in memory. It uses a watcher to determine when files change, as to only re-lint what is necessary.

## Usage

In order to use esprint, first place an `.esprintrc` file in your project. This is similar to a `.flowconfig`. The `.esprintrc` file describes
which paths to lint, which paths to ignore, as well as (optionally) what port to start a lint server on, and how many threads to use when linting.
A sample `.esprintrc` file is shown as follows:

```js
{
  "port": 5004 ,
  "workers": 4,
  "paths": [
      "foo/*.js",
      "bar/**/*.js",
    ],

  "ignored": [
      "**/node_modules/**/*"
    ]
}
```

To run the esprint server, run the following command:

```
$ esprint
```

If the `port` key is not specified in the `.eslintrc` file, then esprint will run parallelized eslint without standing up a background server.

If the server is running in the background, you can use the following command to stop the background server:

```
$ esprint kill
```

You can run `esprint` from any subdirectory that `.esprintrc` is located in, and it will still properly lint all files as specified.


## Developing for ESprint

In order to use ESprint in your project, clone the repository and install all of the dependencies.

```
$ git clone https://github.com/arthuralee/esprint.git && cd esprint
$ yarn
```

In the ESprint repo, run `yarn link`, and in your project that uses ESprint, run `yarn link esprint`.

After that, run `yarn run deps /path/to/project/` so that esprint installs all eslint-related dependencies.

In a separate tab, you can also run `npm start`. This starts up `babel-watcher`, which will compile your JavaScript.

Then, run ESPrint directly from your `node_modules` folder like so:

```
$ node ./node_modules/esprint/build/cli.js [opts]
```
