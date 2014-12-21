---
layout: post
title:  Getting Started with ES 6
date:   2014-12-21 07:00:25
categories: javascript
image: /assets/article_images/node-split.png
---

## What is ES6

ES6 is the latest specification that provides new syntax and also new objects and functionality to existing objects. While the ES6 specification is not yet finished, it brings with it lot of promise that are worth considering at this stage.

## Backward Compatibility

When it comes to creating on newer technologies, the decision usually boils down to thinking how your app will perform across platforms that have not yet implemented the ES6 syntax and functions. With the right tools, we can start taking advantage of the future versions of JavaScript today. Let us look at some of the options.

### Shims

If you only want to use the new objects and functions, you can use a shim. If you want new syntax, you will need a transpiler (follow below after Shims).

#### Shims in Nodejs

Download the Shim module via npm

<pre>npm install es6-shim</pre>

Then, include the module in your existing node files using the default `require`:

<pre>require('es6-shim');</pre>

That's it! Your objects now have extended functionalities and new objects like `promises` ready for use.

#### Shims in Browsers

Download a shim, here is the one I recommend from Paul Miller: <a href="https://github.com/paulmillr/es6-shim/" target="_blank">es6-shim</a>

Then include the script in your page:

<pre>&lt;script src="location/of/my/es6-shim.js"&gt;&lt;/script&gt;</pre>

That's it!


### Transpilers

Transpilers are source-to-source compilers that, given one format, compile the code to the required another format.
The syntax specification of ES6 is new, supporting template strings interpolation with backticks {{ "(\`)"}}, the `module` system, the `let` keyword, and more.

To achieve compatibility, one can opt for a transpiler that compiles code from ES6 syntax to ES5 - which will run across all browsers and nodejs (ES5 is the current specification).

Below are the popular transpilers:

1. <a href="https://github.com/google/traceur-compiler" target="_blank">Traceur</a>
* <a href="https://6to5.org/index.html" target="_blank">6to5</a>

For our scope, let's try to setup *traceur*.

#### Traceur in Nodejs

Download the Traceur module via npm

<pre>npm install --save traceur</pre>

The idea is to write an entry point for your application as a normal node module. In this entry point you load an ES6 file, which bootstraps your application.

<pre>
//startup.js
export function run() {
 	console.log('Getting started with ES6 transpiler: Traceur');
}
</pre>

Now, create the entry point that will be run with node:

<pre>
//index.js
var traceur = require('traceur');
traceur.require.makeDefault(function(file) {
 	return file.indexOf('node_modules') == -1;
});
require('./index').run();
</pre>

That's it! This is a very transparent implementation by Traceur where you simply start using the ES6 syntax seamlessly. This works because the `traceur.require.makeDefault` function overrides the behavior of default `require` function of nodejs, extending it to implement the transpiling automatically.

Good news is that now you can use ES6 modules in your current node applications (we're mixing ES5 and ES6):

<pre>
//my-existing-module.js
var traceur = require('traceur');

//loading an ES6 file
var test = traceur.require('./test');
</pre>

Notice that in the above example, we did not override the default `require` function of nodejs. We simply used the require function provided by traceur.

#### Traceur in Browsers

Download the Traceur module via npm

<pre>npm install --save traceur</pre>

We will now need the traceur-runtime.js file. After installing traceur, you can find it in your npm directory. This is typically located in /usr/local/lib/node_modules/traceur/bin/traceur-runtime.js. Copy the file so that you can include it within the HTML page.

Then transpile your ES6 module by running the below line on a terminal:

<pre>traceur --out dist/final.js src/index.js</pre>

The HTML:
<pre>
&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;script src="lib/traceur-runtime.js"&gt;&lt;/script&gt;
    &lt;script src="dist/final.js"&gt;&lt;/script&gt;
	    &lt;script&gt;
	      var app = System.get('src/index.js');
	      //app is our ES6 module
	      app.run();
	    &lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
  	&lt;-- Body goes here --&gt;
  &lt;/body&gt;
&lt;/html&gt;
</pre>


## Lastly

It is probably going to take a long time before we can shift to ES6 directly without any of the middle tools - probably a few years or more - so in the meantime the tools will assist in getting started with the new web of tomorrow. Support for ES6 is being constantly added to modern browsers, and it is recommended to keep a check on what works where as a default.