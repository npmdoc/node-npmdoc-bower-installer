# api documentation for  [bower-installer (v1.3.5)](https://github.com/rquadling/bower-installer#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-bower-installer.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-bower-installer) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-bower-installer.svg)](https://travis-ci.org/npmdoc/node-npmdoc-bower-installer)
#### Tool for installing bower dependencies that won't include entire repos

[![NPM](https://nodei.co/npm/bower-installer.png?downloads=true)](https://www.npmjs.com/package/bower-installer)

[![apidoc](https://npmdoc.github.io/node-npmdoc-bower-installer/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-bower-installer_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-bower-installer/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-bower-installer/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-bower-installer/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Bret Little"
    },
    "bin": {
        "bower-installer": "./bower-installer.js"
    },
    "bugs": {
        "url": "https://github.com/rquadling/bower-installer/issues"
    },
    "contributors": [
        {
            "name": "Richard Quadling"
        }
    ],
    "dependencies": {
        "async": "^2.1.4",
        "bower": "^1.8.0",
        "colors": "^1.1.2",
        "glob": "^7.1.1",
        "lodash": "^4.17.2",
        "mkdirp": "^0.5.1",
        "node-fs": "~0.1.7",
        "nopt": "^3.0.6"
    },
    "description": "Tool for installing bower dependencies that won't include entire repos",
    "devDependencies": {
        "jasmine": "^2.5.2",
        "rimraf": "^2.5.4"
    },
    "directories": {
        "test": "test"
    },
    "dist": {
        "shasum": "2e43d126feb77621dc8822499c2b23bf6ee76f93",
        "tarball": "https://registry.npmjs.org/bower-installer/-/bower-installer-1.3.5.tgz"
    },
    "engines": {
        "node": ">=0.10.0"
    },
    "gitHead": "61708248944b44b461104f2afdf6665bd7cdd02a",
    "homepage": "https://github.com/rquadling/bower-installer#readme",
    "keywords": [
        "bower",
        "install",
        "dependencies"
    ],
    "license": "MIT",
    "main": "bower-installer.js",
    "maintainers": [
        {
            "name": "blittle",
            "email": "bret.little@gmail.com"
        },
        {
            "name": "rquadling",
            "email": "RQuadling@GMail.com"
        }
    ],
    "name": "bower-installer",
    "optionalDependencies": {},
    "preferGlobal": true,
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/rquadling/bower-installer.git"
    },
    "scripts": {
        "test": "jasmine JASMINE_CONFIG_PATH=test/jasmine.config.json"
    },
    "version": "1.3.5"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module bower-installer](#apidoc.module.bower-installer)
1.  object <span class="apidocSignatureSpan">bower-installer.</span>installer
1.  object <span class="apidocSignatureSpan">bower-installer.</span>utils

#### [module bower-installer.installer](#apidoc.module.bower-installer.installer)
1.  [function <span class="apidocSignatureSpan">bower-installer.installer.</span>installDependency (deps, pakcfg, cfg, paths, silent, callback)](#apidoc.element.bower-installer.installer.installDependency)
1.  [function <span class="apidocSignatureSpan">bower-installer.installer.</span>removeComponentsDir (callback)](#apidoc.element.bower-installer.installer.removeComponentsDir)

#### [module bower-installer.utils](#apidoc.module.bower-installer.utils)
1.  [function <span class="apidocSignatureSpan">bower-installer.utils.</span>copyFile (source, target, cb)](#apidoc.element.bower-installer.utils.copyFile)
1.  [function <span class="apidocSignatureSpan">bower-installer.utils.</span>deleteFolderRecursive (path)](#apidoc.element.bower-installer.utils.deleteFolderRecursive)
1.  [function <span class="apidocSignatureSpan">bower-installer.utils.</span>getExtension (filename)](#apidoc.element.bower-installer.utils.getExtension)
1.  [function <span class="apidocSignatureSpan">bower-installer.utils.</span>getJSON (path, pathSep, filename)](#apidoc.element.bower-installer.utils.getJSON)
1.  [function <span class="apidocSignatureSpan">bower-installer.utils.</span>getPathByRegExp (filename, paths)](#apidoc.element.bower-installer.utils.getPathByRegExp)
1.  [function <span class="apidocSignatureSpan">bower-installer.utils.</span>hasVariableInPath (path)](#apidoc.element.bower-installer.utils.hasVariableInPath)
1.  [function <span class="apidocSignatureSpan">bower-installer.utils.</span>parsePath (path, map)](#apidoc.element.bower-installer.utils.parsePath)



# <a name="apidoc.module.bower-installer"></a>[module bower-installer](#apidoc.module.bower-installer)



# <a name="apidoc.module.bower-installer.installer"></a>[module bower-installer.installer](#apidoc.module.bower-installer.installer)

#### <a name="apidoc.element.bower-installer.installer.installDependency"></a>[function <span class="apidocSignatureSpan">bower-installer.installer.</span>installDependency (deps, pakcfg, cfg, paths, silent, callback)](#apidoc.element.bower-installer.installer.installDependency)
- description and source-code
```javascript
function installDependency(deps, pakcfg, cfg, paths, silent, callback) {
  var base, other;

  var key = pakcfg.key;
  var options = {};
  if (cfg.options) {
    options = cfg.options;
  } else {
    Object.keys(defaultInstallOptions).forEach(function (key) {
      options[key] = defaultInstallOptions[key];
    });
  }

  // Look for an overriden source
  if (cfg.sources && cfg.sources[key]) {
    // local path, so should work
    deps = cfg.sources[key];
  } else {
    deps = deps.split(',');
  }

  if (deps.options && typeof deps.options === 'object') {
    Object.keys(deps.options).forEach(function (key) {
      if (typeof defaultInstallOptions[key] === 'undefined') {
        console.warn("option " + key + " is not a valid install option");
      } else {
        options[key] = deps.options[key];
      }
    });
  }

  // Check for mapping which will map old file names to new ones
  if (deps.mapping) {
    deps = deps.mapping;
  }

  // Ensure we always are dealing with an array
  if (!_.isArray(deps)) {
    deps = [deps];
  }

  // Install each dependency
  async.each(deps, function (dep, callback) {

    // If the file is an object, it is for mapping (renaming) the source
    // file to a new filename in the destination. Because of this, it
    // does not make sense to do a file glob, just immediately install
    // the file
    if (_.isObject(dep)) {
      installFile(dep, pakcfg, paths, dep, silent, options, callback);
    } else {
      glob(dep, function (err, files) {
        if (err) {
          if (!silent) {
            console.log(('Error globbing \t' + key + ' : ' + dep).red);
            console.log(('\t\t' + err).red);
          }
        } else {
          async.each(files, function (f, callback) {
            installFile(f, pakcfg, paths, dep, silent, options, callback);
          }, callback);
        }
      });
    }
  }, callback);
}
```
- example usage
```shell
...
  pakcfg = {name: key};
}
pakcfg.key = key;

if (cfg && (!cfg.ignore || (cfg.ignore && !_.includes(cfg.ignore, key)))) {
  if (_.isArray(dep)) {
    async.each(dep, function (subDep, callback) {
      installer.installDependency(subDep, pakcfg, cfg, paths, options.silent, callback);
    }, callback);
  } else {
    installer.installDependency(dep, pakcfg, cfg, paths, options.silent, callback);
  }
} else {
  if (!options.silent) {
    console.log(('\tIgnoring: ' + key).yellow);
...
```

#### <a name="apidoc.element.bower-installer.installer.removeComponentsDir"></a>[function <span class="apidocSignatureSpan">bower-installer.installer.</span>removeComponentsDir (callback)](#apidoc.element.bower-installer.installer.removeComponentsDir)
- description and source-code
```javascript
removeComponentsDir = function (callback) {
  utils.deleteFolderRecursive(basePath + pathSep + 'bower_components');
  callback();
}
```
- example usage
```shell
...
    console.error(('Error:').red, err);
  }
} else {
  if (options.remove) {
    if (!options.silent) {
      process.stdout.write('Removing bower_components dir...');
    }
    installer.removeComponentsDir(function (err) {
      if (!options.silent) {
        if (err) {
          process.stdout.write(("Error").red, err);
        } else {
          process.stdout.write(("Finished\r\n").green);
        }
      }
...
```



# <a name="apidoc.module.bower-installer.utils"></a>[module bower-installer.utils](#apidoc.module.bower-installer.utils)

#### <a name="apidoc.element.bower-installer.utils.copyFile"></a>[function <span class="apidocSignatureSpan">bower-installer.utils.</span>copyFile (source, target, cb)](#apidoc.element.bower-installer.utils.copyFile)
- description and source-code
```javascript
function copyFile(source, target, cb) {
  var cbCalled = false;

  var rd = fs.createReadStream(source);
  rd.on("error", function (err) {
    done(err);
  });
  var wr = fs.createWriteStream(target);
  wr.on("error", function (err) {
    done(err);
  });
  wr.on("close", function (ex) {
    done();
  });
  rd.pipe(wr);

  function done(err) {
    if (!cbCalled) {
      cb(err);
      cbCalled = true;
    }
  }
}
```
- example usage
```shell
...
  } catch (error) {
    // We wont need to show log error, if package.json doesnt exist default to download folder
    // console.log(error);
  }
}

if (!fs.lstatSync(f_name).isDirectory() && f_name !== f_path) {
  utils.copyFile(f_name, f_path, function (error) {
    if (!error) {
      if (!silent) {
        console.log(('\t' + key + ' : ' + f_path).green);
      }
    } else {
      if (!silent) {
        console.log(('Error\t' + f + ' : ' + f_path).red);
...
```

#### <a name="apidoc.element.bower-installer.utils.deleteFolderRecursive"></a>[function <span class="apidocSignatureSpan">bower-installer.utils.</span>deleteFolderRecursive (path)](#apidoc.element.bower-installer.utils.deleteFolderRecursive)
- description and source-code
```javascript
function deleteFolderRecursive(path) {
  var files = [];
  if (fs.existsSync(path)) {
    files = fs.readdirSync(path);
    files.forEach(function (file, index) {
      var curPath = path + "/" + file;
      if (fs.statSync(curPath).isDirectory()) { // recurse
        deleteFolderRecursive(curPath);
      } else { // delete file
        fs.unlinkSync(curPath);
      }
    });
    fs.rmdirSync(path);
  }
}
```
- example usage
```shell
...
_.each(installPathFiles, function (file) {

  // if file path has variables like {name} do not create/delete folder
  // the folder will be created later in the installer
  if (!utils.hasVariableInPath(file)) {

    if (options['remove-install-path']) {
      utils.deleteFolderRecursive(file);
    }

    if (!fs.existsSync(file)) {
      fileLib.mkdirSync(file, 0755, true);
    }
  }
});
...
```

#### <a name="apidoc.element.bower-installer.utils.getExtension"></a>[function <span class="apidocSignatureSpan">bower-installer.utils.</span>getExtension (filename)](#apidoc.element.bower-installer.utils.getExtension)
- description and source-code
```javascript
function getExtension(filename) {
  return pathLib.extname(filename || '').slice(1);
}
```
- example usage
```shell
...

    path = utils.parsePath(paths.all, pakcfg) + pathSep + key + subDir;

  } else {
    // Determine the path by regular expression...
    path = utils.getPathByRegExp(f_name, paths)
// ...or by file extension.
|| paths[utils.getExtension(f_name)]

    if (path && typeof path !== 'undefined') {

if (!utils.hasVariableInPath(path)) {
  path += (options.includePackageNameInInstallPath ? pathSep + key : '') + subDir;
}
else {
...
```

#### <a name="apidoc.element.bower-installer.utils.getJSON"></a>[function <span class="apidocSignatureSpan">bower-installer.utils.</span>getJSON (path, pathSep, filename)](#apidoc.element.bower-installer.utils.getJSON)
- description and source-code
```javascript
getJSON = function (path, pathSep, filename) {
  var pakcfg = null;

  // If it is a directory lets try to read from package.json file
  if (fs.lstatSync(path).isDirectory()) {
    var pakpath = path + pathSep + (filename ? filename : 'bower') + '.json';

    // we want the build to continue as default if case something fails
    try {
      // read package.json file
      var file = fs.readFileSync(pakpath).toString('ascii')

      // parse file
      pakcfg = JSON.parse(file);

    } catch (error) {
    }
  }

  return pakcfg;
}
```
- example usage
```shell
...
  key: key
}
        }), function (o, callback) {
var dep = o.dep,
  key = o.key;

var keypath = basePath + pathSep + bower.config.directory + pathSep + key;
var pakcfg = utils.getJSON(keypath, pathSep);
if (!pakcfg) {
  pakcfg = {name: key};
}
pakcfg.key = key;

if (cfg && (!cfg.ignore || (cfg.ignore && !_.includes(cfg.ignore, key)))) {
  if (_.isArray(dep)) {
...
```

#### <a name="apidoc.element.bower-installer.utils.getPathByRegExp"></a>[function <span class="apidocSignatureSpan">bower-installer.utils.</span>getPathByRegExp (filename, paths)](#apidoc.element.bower-installer.utils.getPathByRegExp)
- description and source-code
```javascript
function getPathByRegExp(filename, paths) {
  for (var key in paths) {
    if (!paths.hasOwnProperty(key)) {
      continue;
    }

    if (key.indexOf("/") === 0
      && key.lastIndexOf("/") > 0) {
      // Assume the key is a RegExp formatted string.
      var regExp = new RegExp(key.substring(1, key.lastIndexOf("/")));
      if (filename.match(regExp)) {
        return paths[key];
      }
    }
  }

  return null;
}
```
- example usage
```shell
...
  // If the configured paths is a map, use the path for the given file extension
  if (paths.all) {

    path = utils.parsePath(paths.all, pakcfg) + pathSep + key + subDir;

  } else {
    // Determine the path by regular expression...
    path = utils.getPathByRegExp(f_name, paths)
// ...or by file extension.
|| paths[utils.getExtension(f_name)]

    if (path && typeof path !== 'undefined') {

if (!utils.hasVariableInPath(path)) {
  path += (options.includePackageNameInInstallPath ? pathSep + key : '') + subDir;
...
```

#### <a name="apidoc.element.bower-installer.utils.hasVariableInPath"></a>[function <span class="apidocSignatureSpan">bower-installer.utils.</span>hasVariableInPath (path)](#apidoc.element.bower-installer.utils.hasVariableInPath)
- description and source-code
```javascript
hasVariableInPath = function (path) {
  return path.indexOf('{') !== -1;
}
```
- example usage
```shell
...
      function (path) {
return (basePath + pathSep + path);
      });
    _.each(installPathFiles, function (file) {

      // if file path has variables like {name} do not create/delete folder
      // the folder will be created later in the installer
      if (!utils.hasVariableInPath(file)) {

if (options['remove-install-path']) {
  utils.deleteFolderRecursive(file);
}

if (!fs.existsSync(file)) {
  fileLib.mkdirSync(file, 0755, true);
...
```

#### <a name="apidoc.element.bower-installer.utils.parsePath"></a>[function <span class="apidocSignatureSpan">bower-installer.utils.</span>parsePath (path, map)](#apidoc.element.bower-installer.utils.parsePath)
- description and source-code
```javascript
parsePath = function (path, map) {
  if (path.indexOf('{') !== -1) {

    var keys = path.match(KEYS_MATCH);

    _.each(keys, function (key) {
      var p = key.match(KEY_NAME);
      key = p[1];

      var val = key in map ? map[key] : '';
      path = path.replace(new RegExp('\\{[ ]?' + key + '[ ]?\\}', 'gi'), val);

    });
  }
  return path;
}
```
- example usage
```shell
...
    subDir = (f_name_helper[1] != '') ? pathLib.dirname(f_name_helper[1]) : f_name_helper[1];
  }
}

// If the configured paths is a map, use the path for the given file extension
if (paths.all) {

  path = utils.parsePath(paths.all, pakcfg) + pathSep + key + subDir;

} else {
  // Determine the path by regular expression...
  path = utils.getPathByRegExp(f_name, paths)
    // ...or by file extension.
    || paths[utils.getExtension(f_name)]
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
