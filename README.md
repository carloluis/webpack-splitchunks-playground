This repo is set up to explore how to configure webpack 4 to remove chunks from
a list of bundles from every other bundle. This is currently not working as
desired.

To work with this repo, clone it and then

```sh
npm i
npm run build
```

The desired result is for any chunk that appears in `bundles/core.js` or
`bundles/core-b.js` to not appear in any other bundle (and also not be moved to
a separate asset).

[Relevant StackOverflow question](https://stackoverflow.com/questions/49163684/how-to-configure-webpack-4-to-prevent-chunks-from-list-of-entry-points-appearing)

----

## Previous build
> original webpack config `webpack.config.so.js`

```bash
npm run build
```

```
Version: webpack 4.1.1
Time: 758ms
Built at: 3/11/2018 6:00:15 PM
            Asset      Size  Chunks                    Chunk Names
   core.bundle.js   605 KiB       0  [emitted]  [big]  core
  coreB.bundle.js   605 KiB       1  [emitted]  [big]  coreB
      a.bundle.js   606 KiB       2  [emitted]  [big]  a
      b.bundle.js   606 KiB       3  [emitted]  [big]  b
runtime.bundle.js  4.93 KiB       4  [emitted]         runtime
```

## Current build
> new webpack config `webpack.config.js`

```bash
npm run dedup
```

```
Hash: 2dd23dbb1dd6d40b6d2a
Version: webpack 4.1.1
Time: 593ms
Built at: 3/11/2018 6:08:05 PM
              Asset       Size  Chunks                    Chunk Names
     core.bundle.js  953 bytes       0  [emitted]         core
    coreB.bundle.js  964 bytes       1  [emitted]         coreB
        a.bundle.js   1.53 KiB       2  [emitted]         a
        b.bundle.js   1.54 KiB       3  [emitted]         b
  vendors.bundle.js    604 KiB       4  [emitted]  [big]  vendors
a~b~coreB.bundle.js  161 bytes       5  [emitted]         a~b~coreB
 a~b~core.bundle.js  159 bytes       6  [emitted]         a~b~core
  runtime.bundle.js   4.93 KiB       7  [emitted]         runtime
```
