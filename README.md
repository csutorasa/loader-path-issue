# Loader path issue

## Expected Behaviour

Loaders work if the path contains `#` character.

### Actual Behaviour

Webpack build fails with ERROR:

```
assets by status 2.39 KiB [cached] 1 asset
runtime modules 657 bytes 3 modules
built modules 93 bytes [built]
  ../../a#/loader-path-issue/src/index.js 54 bytes [built] [code generated]
  ../../a#/loader-path-issue/src/index.css 39 bytes [not cacheable] [built] [code generated] [1 error]

ERROR in ../../a#/loader-path-issue/src/index.css
Module build failed (from ../../a#/loader-path-issue/node_modules/css-loader/dist/cjs.js):
Error: Cannot find module 'C:\a#\loader-path-issue\node_modules\css-loader\dist\cjs.js'
Require stack:
- C:\a#\loader-path-issue\node_modules\loader-runner\lib\loadLoader.js
- C:\a#\loader-path-issue\node_modules\loader-runner\lib\LoaderRunner.js
- C:\a#\loader-path-issue\node_modules\webpack\lib\NormalModule.js
- C:\a#\loader-path-issue\node_modules\webpack\lib\NormalModuleFactory.js
- C:\a#\loader-path-issue\node_modules\webpack\lib\Compiler.js
- C:\a#\loader-path-issue\node_modules\webpack\lib\webpack.js
- C:\a#\loader-path-issue\node_modules\webpack\lib\index.js
- C:\a#\loader-path-issue\node_modules\webpack-cli\lib\webpack-cli.js
- C:\a#\loader-path-issue\node_modules\webpack-cli\bin\cli.js
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:880:15)
    at Function.Module._load (internal/modules/cjs/loader.js:725:27)
    at Module.require (internal/modules/cjs/loader.js:952:19)
    at require (C:\a#\loader-path-issue\node_modules\v8-compile-cache\v8-compile-cache.js:159:20)
    at loadLoader (C:\a#\loader-path-issue\node_modules\loader-runner\lib\loadLoader.js:19:17)
    at iteratePitchingLoaders (C:\a#\loader-path-issue\node_modules\loader-runner\lib\LoaderRunner.js:182:2)
    at runLoaders (C:\a#\loader-path-issue\node_modules\loader-runner\lib\LoaderRunner.js:395:2)
    at NormalModule.doBuild (C:\a#\loader-path-issue\node_modules\webpack\lib\NormalModule.js:631:3)
    at NormalModule.build (C:\a#\loader-path-issue\node_modules\webpack\lib\NormalModule.js:775:15)
    at C:\a#\loader-path-issue\node_modules\webpack\lib\Compilation.js:1236:12
 @ ../../a#/loader-path-issue/src/index.js 1:0-30
webpack 5.11.1 compiled with 1 error in 181 ms
```

### Steps to Reproduce the Problem

On Windows 10 with run these commands in PowerShell (tested with 5.1):

```powershell
mkdir C:\a#
cd C:\a#
git clone https://github.com/csutorasa/loader-path-issue.git
cd loader-path-issue
npm install
.\node_modules\.bin\webpack
# if webpack fails set execution policy and run the last command again
# Set-ExecutionPolicy Bypass -Scope Process -Force
```

On Linux run these commands in bash (tested with 5.0.17):

```shell
mkdir -p ~/a#
cd ~/a#
git clone https://github.com/csutorasa/loader-path-issue.git
cd loader-path-issue
npm install
node_modules/.bin/webpack
```
