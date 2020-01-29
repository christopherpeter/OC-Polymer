# \<OC-Polymer\>

application to collect nippon data

## Install the Polymer-CLI

First, make sure you have the [Polymer CLI](https://www.npmjs.com/package/polymer-cli) installed. Then run `polymer serve` to serve your application locally.

## Viewing Your Application

```
$ polymer serve
```

## Building Your Application

```
$ polymer build
```

This will create builds of your application in the `build/` directory, optimized to be served in production. You can then serve the built versions by giving `polymer serve` a folder to serve from:

```
$ polymer serve build/default
```

## Running Tests

```
$ polymer test
```
Project setup
npm init
Give your project a name etc then install our dependencies:

npm i --save @polymer/lit-element
npm i --save @webcomponents/webcomponentsjs
npm i --save-dev polyserve
npm i --save-dev webpack
npm i --save-dev webpack-cli

Creating our element
The boilerplate for our element is below:

import { LitElement, html } from '@polymer/lit-element';

class NewMarquee extends LitElement {
constructor()
{
      super();
}
static get properties()
{
    return {}
}
_render(properties)
{
    return html`
    <div><slot></slot></div>
    `;
}
}
window.customElements.define('new-marquee', NewMarquee);


A quick recap of the above, we import the base class LitElement, add a render function where we will put our HTML, and finally define a new element.
We will see what the<slot> tag does later.
Tagged templates
TLDR; the html function in render accepts a template as input and transforms it by doing some clever stuff.
Main HTML page
As web components are part of the web spec, using them is easy:
<html>
<body>
  <script src="node_modules/@webcomponents/webcomponentsjs/webcomponents-bundle.js"></script>
   <new-marquee>My text here</new-marquee>
   <script type="module" src="dist/main.js" crossorigin></script>
</body>
</html>
Unfortunately we reference LitElement by its package name, and as browsers don’t know how to handle this yet we will use Webpack to do the heavy lifting for us:
//webpack.conf.js
module.exports = {
    entry : './new-marquee.js',
    output : {
        filename : 'main.js',
    },
    mode : 'development'
};


To make life easy lets add some scripts to package.json:

"serve": "polyserve",
"webpack": "webpack --config webpack.conf.js",
"start": "npm run-script webpack && npm run-script serve",


We use Polyserve as a simple server (any will do) and Webpack to pack our JS.

To see our code in action:
npm start

Then navigate to the page displayed on the command line. Notice that the text we put inside our new element appears on screen? The <slot> element allows us to use any elements put inside our custom one.
