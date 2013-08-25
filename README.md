# npm-fetch

Fetch npm modules.  **This is a work in progress.**

[![Build Status](https://travis-ci.org/ForbesLindesay/npm-fetch.png?branch=master)](https://travis-ci.org/ForbesLindesay/npm-fetch)
[![Dependency Status](https://gemnasium.com/ForbesLindesay/npm-fetch.png)](https://gemnasium.com/ForbesLindesay/npm-fetch)
[![NPM version](https://badge.fury.io/js/npm-fetch.png)](http://badge.fury.io/js/npm-fetch)

## Usage

```js
var fetch = require('npm-fetch');
fetch('npm-fetch@0.0.1', __dirname + '/npm-fetch.tgz', function (err) {
  if (err) throw err;
})
```

## API

### fetch(name, spec, dest, options, cb)

**UNSTABLE**

Fetch the package as a tarball to destination using the appropriate method.

 - `name` the name of the package as a string
 - `spec` a string which can be:
   - a version, version range or tag if the module is in the npm repository
   - a url with `https` or `http` as the scheme, where the module is hosted somewhere as a tarball
   - a git url, where the module will be cloned as a git repository
   - a GitHub specifier of the form `username/reponame#tag-name` where `#tag-name` is optional and defaults to `#master`
   - a path to a local file or folder

### npm.version(name, version, options)

Download package at exact version and return a stream.

### npm.range(name, versionRange, options)

Not yet implemented

### npm.tag(name, tag, options)

Download the package `name` at `tag` and return a stream

### github(name, 'user/repo#tag', options)

Returns a stream for the GitHub repo as a tarball at the given tag (defaults to master)

e.g.

```js
fetch.github('npm-fetch', 'ForbesLindesay/npm-fetch', {})
  .pipe(fs.createWriteStream('npm-fetch.tar.gz'))
```

### git(name, url, options)

Not yet implemented

### tarball(name, url, options)

Get a stream for a tarball (handling redirects and retries).

### local.dir(name, path, options)

Package up the directory at path and return a stream for the tarball.

### local.file(name, path, options)

Just create a read stream for `path`
