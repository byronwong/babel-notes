# Getting started with Babel

## Calling Babel from local
In order to run Babel locally you will need to run Babel from the `.bin` folder.

Once in you project folder run: `node_modules/.bin/babel --version`


## Running Babel
To run use: `babel src`

Notice we can pass it folders to execute on.

Notice running Babel on the code does not actually transpile the code, we will need to install the additional plugin to activate the transpilation.

Use: `npm i -D babel-preset-es2015`

We then need to tell Babel to use the plugin.

Use: `babel src --presets es2015`

We can also output the code into a directory

Use: `babel src --presets es2015 --out-dir build` or use: `-d` flag

If we have multiple files we can combine them using the `--out-file` or `-o`

Use: `babel src --presets es2015 --out-file build/bubdle.js -s`

Use: `-s` to generate source maps

Use: `-w` to get babel cli to watch files

This is now getting long, now it's time to use a config file.

## Using a config
Allows us to establish defaults so we don't have to retype all the time. 

Use can also down the individual plugins and only whats need by going to the website. These are now included in the babelrc file and the presets section has been deleted.

## Tranoiling to different module types
[Babel Plugins](https://babeljs.io/docs/plugins/)
AMD, Common JS, UMD, System JS. Here we will be transpiling ES6 modules to supported verions 

## Babel in your build
