
## Automating Website Optimizations

* [Introduction](../)
* [Grunt](../grunt/)
* [Grunt plugins](../grunt-plugins/)
* » [h5bp/node-build-script](../node-build-script/)

---

```js
{
  "author": "Mickael Daniel",
  "github": "http://github.com/mklabs",
  "twitter": "@mklabs",
  "date": "new Date('Mon Apr 10 2012 19:00:00 GMT+0200')"
  "dependencies": {
    "your-attention": "1.0.0"
  }
}
```

## h5bp/node-build-script

* https://github.com/h5bp/node-build-script

* Port of [ant-build-script](https://github.com/h5bp/ant-build-script)

## A Grunt Plugin

* Now a Grunt Plugin (plugins were introduced in grunt 0.3.x)

* Still very early stage of development

## A Grunt Plugin - Install

*1. Install the plugin*

```sh
# next to your project's gruntfile
$ npm install http://nodeload.github.com/h5bp/node-build-script/tarball/master
```

*2. Add the plugin as a project dependency in your package.json*

```javascript
"dependencies": {
  "node-build-script": "http://nodeload.github.com/h5bp/node-build-script/tarball/master"
}
```

### A Grunt Plugin - Install

Load the plugin tasks - In your gruntfile:

```js
...
// Load the plugin tasks and helpers
grunt.loadNpmTasks('node-build-script')

// Default task.
grunt.registerTask('default', 'lint qunit concat min');
...
```

### A Grunt Plugin - Usage

```sh
$ grunt --help
```

### A Grunt Plugin - Tasks

* **clean**: Wipe the previous build dirs.
* **mkdirs**: Prepares the build dirs.
* **css**: Concats, replaces @imports and minifies CSS files.
* **rev**: Automate the revving of assets and perform the hash rename
* **usemin**: Replaces references to non-minified scripts / stylesheets

### A Grunt Plugin - Tasks

In addition to those tasks,
there are a few additional tasks to help you in the process:

* **serve**: Spawns up a basic local http server (on both pubilsh /
  intermediate folder with different ports).

* **connect**:  Spawns up local http sever with socket.io configured,
  it'll inject a tiny client side script + socket.io lib on `*.html`
  response.

* **reload**: Alias for `connect watch:reload`.

### socket.io + watch combo

Gives you a great development environment

* Automatically reloads your browser whenever a file changes

* Might re-trigger a given task before reloading
  * like re-running the entire build script
  * Re-run preprocessors (CoffeeScript, Less, Sass, w/e)

### socket.io + watch combo

**process and build script needs to be almost immediate in this context**

and node is a pretty good candidate for that :p

### An experimental JSDOM based build script

The idea grown and original came from @necolas [proposal](https://github.com/h5bp/html5-boilerplate/issues/831).

DOM-based build script can tremendously reduce the amount of configuration.

If not simply removing the need of confirmation.

### An experimental JSDOM based build script

* Ideally...

### An experimental JSDOM based build script

* It just works!

### An experimental JSDOM based build script

**How it works**

https://github.com/h5bp/node-build-script/wiki/dom

* Works with "plugins"

### JSDOM based - Plugins

A plugin is a special jQuery "plugin" that can use the node (or grunt) api to do
their task.

The following plugins are implemented

* **css**
Relies on @import statement mainly which are inlined (with nested path
rewrite) to serve a single optimized stylesheet.

* **js**
Concat, minify through uglify and serve a single concat'd / minified script.


### JSDOM Based - Configuration

```js
var h5bp = require("node-build-script");

module.exports = function(grunt) {

  grunt.initConfig({
      ...,

      dom: {
          files: ["*.html", "views/**/*.html"],
          "script[data-build]"    : h5bp.plugins.script,
          "link"                  : h5bp.plugins.link,
          "img"                   : h5bp.plugins.img,
          "script, link, img"     : h5bp.plugins.rev
      },

      ...
  });

};
```

### next h5bp/node-build-script

* Windows support for dom based build

* Manifest generation using [confess](https://github.com/jamesgpearce/confess)
  and [phantomjs](https://github.com/ariya/phantomjs)

* Sourcemap generation
  * with google closure compiler, until we have a valid node-based solution*
  * [mozilla/sourcemap](https://github.com/mozilla/source-map) might be a pretty good start

### next h5bp/node-build-script

* Better and more h5bp init templates.

* Further integration in init templates of well-known project
  like [twitter/bootstrap](https://github.com/twitter/bootstrap)
  or [zurb/foundation](https://github.com/zurb/foundation).

### next h5bp/node-build-script

* inline small images as data-uri
* remove console.log and other debugger statements
* cache manifest creation
* (how?) remove unused CSS
* (how?) dead code elimination
* image compression
* (how) video/audio transcoding


### Try it yourself

See the [gist](https://gist.github.com/2359881)

> https://gist.github.com/2359881#file_install.sh

```sh
$ curl https://raw.github.com/gist/2359881/install.sh | sh
```
