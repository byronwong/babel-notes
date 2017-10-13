# Getting started with Babel

<!-- TOC -->

- [Getting started with Babel](#getting-started-with-babel)
    - [Installing Babel](#installing-babel)
        - [Calling Babel from local](#calling-babel-from-local)
    - [Running Babel](#running-babel)
    - [Installing Presets](#installing-presets)
        - [Using Presets](#using-presets)
        - [Creating a config file](#creating-a-config-file)
        - [Module Formatters](#module-formatters)
        - [Polyfills and Shims](#polyfills-and-shims)
    - [Browser Support](#browser-support)
        - [Babel polyfill](#babel-polyfill)
        - [Supporting IE8](#supporting-ie8)
    - [Using Babel with your build tools](#using-babel-with-your-build-tools)
        - [NPM scripts](#npm-scripts)
        - [Gulp](#gulp)
    - [Module loaders](#module-loaders)
        - [Webpack](#webpack)
        - [Browserify](#browserify)
        - [React](#react)
    - [Resources](#resources)

<!-- /TOC -->

> NOTE: We will be using the latest version where babel has been divided into modules. 

## Installing Babel
Globally 
> `npm i -g babel-cli`

Locally 
> `npm i -D`

Check (using REPL)
> `babel --version`

### Calling Babel from local
In order to run Babel locally you will need to run Babel from the `.bin` folder.
Once in you project folder run: `node_modules/.bin/babel --version`

> `npm i -D babel-cli`
> `node_modules/.bin/babel --version`

## Running Babel
- To run use: `babel src`
- Notice we can pass it folders to execute on.


## Installing Presets
- The babel cli does not do any transpilation, in the newer version of babel the code has been modularised
- To start transpilation we can install the es2015 `preset` (module bundle).
- Use: `npm i -D babel-preset-es2015`


### Using Presets
In oder to use babel at a very basic level we will need to supply it the preset. 
> `babel src --presets es2015`

We can also output the code into a directory using `--out-dir`.
> `babel src --presets es2015 --out-dir build` or using: `-d` flag.

If we have multiple files we can combine them using the `--out-file` or `-o`.
- We will specify the directory via the path and the new file name.
> `babel src --presets es2015 --out-file build/bundle.js`

Additionally:
- Use: `-s` to generate source maps.
- Use: `-w` to get babel cli to watch files.
> Example: `babel src --presets es2015 -o build/bundle.js -s -w`

This is now getting long, now it's time to use a config file.


### Creating a config file
- Allows us to establish defaults. 
- In the babelrc file we can define the preset we want to use. (see `babelrc`)
- Thus in our command line we no longer need to define the preset.
> Example: `babel src -o build/bundle.js -s -w`

- We can also move the sourcemaps flag into to rc-file.
> Example: `babel src -o build/bundle.js -w`

- Additionally we can define individual `plugins` if we want a customize babel.
- We would need to npm install them first.
- and then in our babelrc file:
```json
    "plugins": [
        "transform-es2015-modules-amd", 
        "transform-es3-member-expression-literals",
        "transform-es3-property-literals"
    ]
```

### Module Formatters
- [Babel Plugins](https://babeljs.io/docs/plugins/)
- Babel can transpile your code to your target module format: AMD, Common JS, UMD, System JS. 
- You will need to download the module formatter `plugin` (please see rc file).
- If you are using the `es2015` preset commonJS is already loaded.


### Polyfills and Shims 
- [Polyfill Docs](https://babeljs.io/docs/usage/polyfill/)
- Babel comes with polyfills to support older browsers, we will need to include this in our code.
> `<script src="../node_modules/babel-polyfill/dist/polyfill.min.js"><script>`
> `npm i babel-poly-fill -S` 

---

## Browser Support

### Babel polyfill
- Allows you to support ES5,6,7, features from IE9+ that transpiling does not fix.
- You can install the babel polyfill from npm, 
- however to use it you will need to link to it using a `<script>` tag in your html

### Supporting IE8
- To support IE8 you will need to do all of the above 
- And also look at the [ES3 plugins](https://babeljs.io/docs/plugins/) 

---

## Using Babel with your build tools

### NPM scripts
- Under the scripts section, create a script e.g. `"demo"`.
- For this let's do something simple: `"babel --version"`.
- As usual we run `npm run demo` from the terminal.

### Gulp
- npm install `gulp-babel` and follow instruction on npm.
- You may want to write your gulp file in ES6 itself. 
- If you are using the recent version of node.js it will work.
- However if you are using an older version of node follow steps below.
- Rename your `gulpfile.js` to `gulpfile.babel.js`
- Npm install the `babel-core`
- Now run gulp - this should work now.

## Module loaders

### Webpack
- npm install webpack globally and locally
- to run as cli: `webpack <entry-file/location> <output-file/location>` 
- Create a `webpack.config.js` 
- npm i `babel-loader` and `babel-core`.
```js
// webpack config.js
module.exports = {
    entry: './src/your/path/main.js', // js entry file
    output: {
        path: './dist',
        filename: 'bundle.js'
    },
    module: {
        loaders: [
            {
                test: /\.js$/, // check for valid files
                exclude: /node_modules/, // do use files from...
                loader: 'babel-loader' // loader to use
            }
        ]
    }
}
```
- Then just run `webpack` default command. 


### Browserify
- Is also a module loader like webpack
- To install npm i `browserify` `-g -D`
- Create a output folder e.g. `dist`
- Add babel by `npm i babelify -D`
- CLI: `browserify --entry src/app.js --outfile dist/bundle.js --transform babelify`
- CLI shorthand: `browserify -e src/app.js -o dist/bundle.js -t babelify`

### React
TBC


## Resources
[Kangax table](https://kangax.github.io/compat-table/es6/)
