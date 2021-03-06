[![Build Status](https://travis-ci.org/softbrix/stureby-index.svg?branch=master)](https://travis-ci.org/softbrix/stureby-index)

# Stureby Index

This is a simple index or cache for javascript.

Install the module simply with npm or yarn

```
npm i --save stureby-index
```

or

```
yarn add stureby-index
```

Create the index instance by simply requiring the stureby-index module and create a
new instance of the object.

```
var shIndex = require('stureby-index');
const idx = shIndex(idxPath);
```

Then you can use the put, get and search methods to modify the index.

```
idx.put('as', 'the beste1');
idx.put('asa', 'the beste2');
idx.put('asas', 'the beste3');
idx.put('asasas', 'the beste4');
console.log(idx.get('asasas')) // 'the beste4'
```

The first argument to the put method is the key and the second is the value.
The same key can be linked to multiple values.

The search method will return a list of matched keys.

```
console.log(idx.search('asas')); // ['asas', 'asasas']
```

### Example of flush before process exists

You need to add the following code in your node project to secure one last flush if the process exits normally.

```
  if(!_.isUndefined(process)) {
    process.on('SIGINT', indexObject.flush);
  }
```

If the process exits in an uncertain situation (ie, application crash or power loss) then the data written to the cache since last flush is lost.

### Options

* storageFactory (undefined) - override the persistant storage to use
* flushTime (500) - the time in milliseconds between flushing changes back to persisted storage
* persist (true) - should we persist the index to file or just keep it in memory

# Changelog

## Version 3

This version has an internal cache for the open indexes so if you try to access the same path from different parts of the code in the same javascript vm you will write and read from a single instance.

This version adds the following methods:

- size()

## Version 2

The new version is backwards compatible with version 1 of the index. The index
will be upgraded and once it is flushed back to disk the process is not reversible.

This version adds the following methods:

- toJSON()
- delete(key)
- clear()

### Don't persist on disk

In this version it is possible to create a index without the disk access. The
options parameter should include persist false which will use the noop_storage.

## Why Stureby?

Stureby is a small area in the southern suburbs of Stockholm, Sweden. This is a
calm and child friendly area having mostly small houses and private villas.
This is the place where my mother spent her first year with her family and where
I currently live with mine.
