# api documentation for  [gulp-livereload (v3.8.1)](https://github.com/vohof/gulp-livereload#readme)  [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-livereload.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-livereload)
#### Gulp plugin for livereload.

[![NPM](https://nodei.co/npm/gulp-livereload.png?downloads=true)](https://www.npmjs.com/package/gulp-livereload)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-livereload/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp_livereload_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-livereload/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-gulp-livereload/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "bugs": {
        "url": "https://github.com/vohof/gulp-livereload/issues"
    },
    "dependencies": {
        "chalk": "^0.5.1",
        "debug": "^2.1.0",
        "event-stream": "^3.1.7",
        "gulp-util": "^3.0.2",
        "lodash.assign": "^3.0.0",
        "mini-lr": "^0.1.8"
    },
    "description": "Gulp plugin for livereload.",
    "devDependencies": {
        "mocha": "^2.0.1",
        "sinon": "^1.12.2"
    },
    "directories": {},
    "dist": {
        "shasum": "00f744b2d749d3e9e3746589c8a44acac779b50f",
        "tarball": "https://registry.npmjs.org/gulp-livereload/-/gulp-livereload-3.8.1.tgz"
    },
    "gitHead": "0debe6fc3f39560aaf7a79daed04fa4aa8080e75",
    "homepage": "https://github.com/vohof/gulp-livereload#readme",
    "keywords": [
        "gulpplugin",
        "livereload"
    ],
    "license": "MIT",
    "main": "./index.js",
    "maintainers": [
        {
            "name": "vohof",
            "email": "david@jcyr.us"
        }
    ],
    "name": "gulp-livereload",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/vohof/gulp-livereload.git"
    },
    "scripts": {
        "test": "mocha"
    },
    "version": "3.8.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-livereload](#apidoc.module.gulp-livereload)
1.  [function <span class="apidocSignatureSpan">gulp-livereload.</span>changed (filePath)](#apidoc.element.gulp-livereload.changed)
1.  [function <span class="apidocSignatureSpan">gulp-livereload.</span>listen (opts, cb)](#apidoc.element.gulp-livereload.listen)
1.  [function <span class="apidocSignatureSpan">gulp-livereload.</span>middleware (opts)](#apidoc.element.gulp-livereload.middleware)
1.  [function <span class="apidocSignatureSpan">gulp-livereload.</span>reload (filePath)](#apidoc.element.gulp-livereload.reload)
1.  object <span class="apidocSignatureSpan">gulp-livereload.</span>options



# <a name="apidoc.module.gulp-livereload"></a>[module gulp-livereload](#apidoc.module.gulp-livereload)

#### <a name="apidoc.element.gulp-livereload.changed"></a>[function <span class="apidocSignatureSpan">gulp-livereload.</span>changed (filePath)](#apidoc.element.gulp-livereload.changed)
- description and source-code
```javascript
changed = function (filePath) {
  if (!exports.server) {
    debug('no server listening, nothing notified.');
    return;
  }
  if (typeof filePath === 'object') {
    filePath = filePath.path;
  }
  if (options.basePath) {
    filePath = '/' + relative(options.basePath, filePath);
  }

  exports.server.changed({ body: { files: [ filePath ] } });

  if (!options.quiet) {
    gutil.log(magenta(filePath) + ' reloaded.');
  }
}
```
- example usage
```shell
...

Creates a stream which notifies the livereload server on what changed.

### livereload.listen([options])

Starts a livereload server. It takes an optional options parameter that is the same as the one noted above. Also you dont need to
 worry with multiple instances as this function will end immidiately if the server is already runing.

### livereload.changed(path)

Alternatively, you can call this function to send changes to the livereload server. You should provide either a simple string or
 an object, if an object is given it expects the object to have a 'path' property.

> NOTE: Calling this function without providing a 'path' will do nothing.

### livereload.reload([file])
...
```

#### <a name="apidoc.element.gulp-livereload.listen"></a>[function <span class="apidocSignatureSpan">gulp-livereload.</span>listen (opts, cb)](#apidoc.element.gulp-livereload.listen)
- description and source-code
```javascript
listen = function (opts, cb) {
  if (exports.server) return;

  if (typeof opts === 'number') {
    opts = { port: opts };
  } else if (typeof opts === 'function') {
    cb = opts;
    opts = {};
  }

  options = _assign(options, opts);
  exports.server = new minilr.Server(options);
  exports.server.listen(options.port, options.host, function() {
    debug('now listening on port %d', options.port);
    if(typeof cb === 'function') cb.apply(exports.server, arguments);
  });
}
```
- example usage
```shell
...
  gulp.src('less/*.less')
    .pipe(less())
    .pipe(gulp.dest('css'))
    .pipe(livereload());
});

gulp.task('watch', function() {
  livereload.listen();
  gulp.watch('less/*.less', ['less']);
});
'''

**See [examples](examples)**.

API & Variables
...
```

#### <a name="apidoc.element.gulp-livereload.middleware"></a>[function <span class="apidocSignatureSpan">gulp-livereload.</span>middleware (opts)](#apidoc.element.gulp-livereload.middleware)
- description and source-code
```javascript
function middleware(opts) {
  var srv = new Server(opts);
  servers.push(srv);
  return function minilr(req, res, next) {
    srv.handler(req, res, next);
  };
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp-livereload.reload"></a>[function <span class="apidocSignatureSpan">gulp-livereload.</span>reload (filePath)](#apidoc.element.gulp-livereload.reload)
- description and source-code
```javascript
reload = function (filePath) {
    exports.changed(filePath || options.reloadPage);
}
```
- example usage
```shell
...

### livereload.changed(path)

Alternatively, you can call this function to send changes to the livereload server. You should provide either a simple string or
 an object, if an object is given it expects the object to have a 'path' property.

> NOTE: Calling this function without providing a 'path' will do nothing.

### livereload.reload([file])

You can also tell the browser to refresh the entire page. This assumes the page is called 'index.html', you can change it by providing
 an **optional** 'file' path or change it globally with the options 'reloadPage'.

###  livereload.middleware

You can also directly access the middleware of the underlying server instance (mini-lr.middleware) for hookup through express, connect
, or some other middleware app
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
