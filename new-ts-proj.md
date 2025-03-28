# New TS proj

_Status: Published_
_Created: 2023-03-08 15:41:01_

```
npm init
```

```
npm install npm@latest -g
```

```
tsc --init --sourceMap --rootDir src --outDir dist
```
```
mkdir src
cd src
touch index.ts
```
npm i save-dev typescript
point source in tsconfig.json to the outDir: dist &  rootDir: src

add another ts file

compile with
```
 tsc
```
package.json
"main": "index.js"


intellij set language to typescipt in settings
recompile on changes


