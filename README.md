# relative [![NPM version](https://badge.fury.io/js/relative.svg)](http://badge.fury.io/js/relative)

> Get the relative filepath from path A to path B. Calculates from file-to-directory, file-to-file, directory-to-file, and directory-to-directory.

**Calculates correctly from:**

* file-to-directory
* file-to-file
* directory-to-file
* directory-to-directory

## Install with [npm](npmjs.org)

```bash
npm i relative --save
```

## Usage

```js
var relative = require('relative');
relative(from, to);

relative('a/b/c.txt', 'd');
//=> '../../d'

relative('d', 'a/b/c.txt');
//=> '../a/b/c.txt'
```

Relative to `process.cwd()`

```js
relative('a/b/c.txt');
//=> 'a/b/c.txt'

relative(process.cwd(), 'a/b/c.txt');
//=> 'a/b/c.txt'

relative('a/b/c.txt', process.cwd());
//=> '..'
```

### stat

There are cases where it is impossible to tell if a path is a file or a directory without more information.

**Examples**

If assume that `a.b.c` is a directory, we have no way of know that without hitting the filesystem, which is impossible if the path doesn't actually exist.

So the result would be:

```js
relative('fixtures/a.b.c', 'fixtures');
//=> '.'
```

**If the path exists**

Pass `true` as the last argument, or pass the stat object from `fs.stat()`/`fs.statSync()` and you will get the correct result.

```js
relative('fixtures/a.b.c', 'fixtures', true);
//=> '..'
```

**If the path does not exist**

End directory names with trailing slash. If you can't or don't want to do that, you may get incorrect results from time to time, but there isn't much we can do about it.

One very bad idea I had was to create a whitelist of filenames that look like directories, and directories that look like file names so that when those paths are encountered the logic would be adjusted accordingly. Anyway, it is what it is.


## relative.toBase()

Get the relative path to the given `base`.

```js
relative.toBase(base, filepath);
```

**Example**:

```js
relative.toBase('a/b', 'a/b/c/d/file.txt');
//=> 'c/d/file.txt'
```

## Other useful libs
 * [cwd](https://github.com/jonschlinkert/cwd): Node.js util for easily getting the current working directory of a project based on package.json or the given path.
 * [export-files](https://github.com/jonschlinkert/export-files): node.js utility for exporting a directory of files as modules.
 * [is-absolute](https://github.com/jonschlinkert/is-absolute): Return true if a file path is absolute.
 * [is-relative](https://github.com/jonschlinkert/is-relative): Returns `true` if the path appears to be relative.
 * [is-dotfile](https://github.com/regexps/is-dotfile): Return true if a file path is (or has) a dotfile.
 * [global-prefix](https://github.com/jonschlinkert/global-prefix): Get the npm global path prefix.

## Running tests
Install dev dependencies:

```bash
npm i -d && npm test
```

## Contributing
Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/relative/issues)

## Author

**Jon Schlinkert**

+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert) 

## License
Copyright (c) 2014-2015 Jon Schlinkert  
Released under the MIT license

***

_This file was generated by [verb-cli](https://github.com/assemble/verb-cli) on April 05, 2015._