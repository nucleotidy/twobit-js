# @gmod/twobit

[![NPM version](https://img.shields.io/npm/v/@gmod/twobit.svg?style=flat-square)](https://npmjs.org/package/@gmod/twobit)
[![Build Status](https://img.shields.io/travis/GMOD/twobit-js/master.svg?style=flat-square)](https://travis-ci.org/GMOD/twobit-js) 

Read .2bit sequence files using pure JavaScript, works in node or in the browser.

## Install

    $ npm install --save @gmod/twobit

## Usage

```js
const { TwoBitFile } = require('@gmod/twobit')
const mytwobit = new TwoBitFile({
  path: require.resolve('./data/foo.2bit'),
})

const chr1Bases = await t.getSequence('chr1', 45, 50)
// chr1Bases is now a string of bases, 'ACTG...'

// get object with all seq lengths as { seqName => length, ... }
const allSequenceSizes = await t.getSequenceSizes()

// get the size of a single sequence
const chr1Size = await t.getSequenceSize('chr1')

// get an array of all sequence names in the file
const seqNames = await t.getSequenceNames()
```

## API

### TwoBitFile

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

##### Table of Contents

-   [constructor](#constructor)
-   [getHeader](#getheader)
-   [getIndex](#getindex)
-   [getSequenceNames](#getsequencenames)
-   [getSeqSizes](#getseqsizes)
-   [getSequenceSize](#getsequencesize)
-   [getSequence](#getsequence)

#### constructor

**Parameters**

-   `args` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `args.filehandle` **Filehandle?** node fs.promises-like filehandle for the .2bit file.
         Only needs to support `filehandle.read(buffer, offset, length, position)`
    -   `args.path` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** filesystem path for the .2bit file to open
    -   `args.seqChunkSize`  

#### getHeader

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)** object with the file's header information, like
 `{ magic: 0x1a412743, version: 0, sequenceCount: 42, reserved: 0 }`

#### getIndex

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)** object with the file's index of offsets, like `{ seqName => fileOffset, ...}`

#### getSequenceNames

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)** an array of string sequence names that are found in the file

#### getSeqSizes

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)** for an object listing the lengths of all sequences as seqName => length

#### getSequenceSize

**Parameters**

-   `seqName` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** 

#### getSequence

**Parameters**

-   `seqName` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** name of the sequence you want
-   `regionStart` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** optional 0-based half-open start of the sequence region to fetch. default 0. (optional, default `0`)
-   `regionEnd` **[number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)?** optional 0-based half-open end of the sequence region to fetch. defaults to end of the sequence

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)** promise for a string of sequence bases

## License

MIT © [Robert Buels](https://github.com/rbuels)
