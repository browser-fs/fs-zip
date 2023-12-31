# BrowserFS Zip Backend

[BrowserFS](https://github.com/browser-fs/core) backend for Zip files.

Please read the BrowserFS documentation!

## Backend

This package adds `ZipFS`, which allows you to create a *readonly* file system from a zip file.

For more information, see the [API documentation](https://browser-fs.github.io/fs-zip).

## Installing

```sh
npm install @browserfs/fs-zip
```

## Usage

> 🛈 The examples are written in ESM. If you are using CJS, you can `require` the package. If running in a browser you can add a script tag to your HTML pointing to the `browser.min.js` and use BrowserFS Zip via the global `BrowserFS_Zip` object.

You can't use ZipFS on its own. You must import the core in order to use the backend, and must register it if you plan on using `configure`:

```js
import { configure, fs, registerBackend } from '@browserfs/core';
import { ZipFS } from '@browserfs/fs-zip';
registerBackend(ZipFS);

const res = await fetch('http://example.com/archive.zip');
const zipData = await res.arrayBuffer();

await configure({ '/mnt/zip': { fs: 'ZipFS', options: { zipData } } });

const contents = fs.readFileSync('/mnt/zip/in-archive.txt', 'utf-8');
console.log(contents);
```
