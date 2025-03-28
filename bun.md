# Bun

_Status: Published_
_Created: 2023-09-18 13:58:34_
_Tags: bun, node, javascript, cli, ng_

# Node Js

- Node team is klein team en onbetaald
- Voortgang Node versies gaat vooral over niet te veel breaken met voorgaande versies
- Hierdoor blijven kritisch perfomance issues liggen
- Gebouwd op de V8 engine. Kijk bv naar de code van de [shell](https://chromium.googlesource.com/v8/v8/+/master/samples/shell.cc)

---
# Bun

- Het Bun team zet in op performance
- Heeft links met React en Vue
- Probeert het hele eco systeem van Node te kunnen draaien
- Kort gezegd een snellere Node

---
# Klachten over Node
- single threaded  & concurrency  
- callbacks  
- Loops
- Limited standard Libs  
- CPU perfomant tasks  & Memory consumption  
- debugging  
- gemopper over update cycle en deprecations


---
# Bun Safari Engine
Safari engine voordelen:  
- batterij  
- performance webkit  
- security  
- CJS and ES6 and beyond support  
- cross-platform  
- kleiner en sneller  
- voor de browser

[Safari](https://github.com/WebKit/WebKit)

---
# Wat is Bun nou?

het staat op : [Bun Home Page](https://bun.sh)
Op Youtube zeggen ze zelf:
- Bun is still under development.
- Use it to speed up your development workflows or run simpler production code in resource-constrained environments like serverless functions. 
- We're working on more complete Node.js compatibility and integration with existing frameworks. 
---
# Wat Bun is nou
- Bun is an all-in-one toolkit for JavaScript and TypeScript apps. It ships as a single executable called `bun​`.  
- At its core is the _Bun runtime_, a fast JavaScript runtime designed as a drop-in replacement for Node.js. 
- It's written in Zig and powered by JavaScriptCore under the hood, dramatically reducing startup times and memory usage.
- Werkt (nog) niet op Windows


---
# Bun Install
  Op Linux achtige machines:
```shell  
# with install script (recommended)  
curl -fsSL https://bun.sh/install | bash  
  
# with npm  
npm install -g bun  
  
# with Homebrew  
brew tap oven-sh/bun  
brew install bun  
  
# with Docker  
docker pull oven/bun  
docker run --rm --init --ulimit memlock=-1:-1 oven/bun  
```
---
# bun init  
Na de check of bun t doet:  
```bash
bun --version  
```
Kan je: 
```bash
bun init
```
---
# Bun commands
Net zoals npm

### upgrade
```bash    
bun upgrade    
```

### To install dependencies:  
  
```bash    
bun install
bun i
```

---
# bun start inhoud folder

*branche 01_init*
na
```bash
bun init
```
bevat de folder 

.gitignore  
README.md  
bun.lockb  
index.ts  
node_modules  
package.json  
tsconfig.json  

---
# Bun run
### hierna klaar voor:
```bash    
bun run index.ts    
``` 
---
# Bun imports
*branche 02_say_hello* 

import van andere ts file 

---
# Bun serve
*branch 03_bun_serve* 

start een server op zoals in bv express 

---
# Bun scripts
*branch 04 bun run start*
```ts
"scripts": {  
  "start": "bun run index.ts"  
},
```

---
# Bun Scripts 2
```json  
{  
  // ... other fields  
  "scripts": {  
    "clean": "rm -rf dist && echo 'Done.'",  
    "dev": "bun server.ts"  
  }  
}  
  
```

```ts  
bun run clean  
bun run dev  
```  
---
# Bun tsconfig

*branch 5 dom en tsconfig*

rare errors van mn lsp kon ik oplossen met:

```ts
/// <reference lib="dom" />  
/// <reference lib="dom.iterable" />
```


---
# Bun run  
  
```bash    
bun run index.ts    
```  
  
To run a file in watch mode, use the `--watch` flag.  
  
```  
bun --watch run index.tsx  
```  

---
# Scripts  
```json  
{  
  // ... other fields  
  "scripts": {  
    "clean": "rm -rf dist && echo 'Done.'",  
    "dev": "bun server.ts"  
  }  
}  
  
```

```ts  
bun run clean  
bun run dev  
```  
---
# Bun test

[Bun pagina Run tests](https://bun.sh/docs/cli/test#run-tests)  
  
```  
bun test  
```  
  
Tests are written in JavaScript or TypeScript with a Jest-like API. Refer to [Writing tests](https://bun.sh/docs/test/writing) for full documentation.  

---
# Bun test 2

The runner recursively searches the working directory for files that match the following patterns:  
  
- `*.test.{js|jsx|ts|tsx}`  
 `*_test.{js|jsx|ts|tsx}`  
- `*.spec.{js|jsx|ts|tsx}`  
- `*_spec.{js|jsx|ts|tsx}`  
  
You can filter the set of _test files_ to run by passing additional positional arguments to `bun test`. 

---
# Test example
* 06_test branche* 
math.test.ts  
  
```  
import { expect, test } from "bun:test";  
  
test("2 + 2", () => {  
  expect(2 + 2).toBe(4);  
});  
```  

---
# Elysia

[Elisia](https://elysiajs.com)
De Express van / met Bun
```bash
bun create elysia app
```
---
# Elysia 2

- Performance : You shall not worry about the underlying performance
- Simplicity :  Simple building blocks to create an abstraction, not repeating yourself
- Flexibility : You shall be able to customize most of the library to fits your need

eenvoudig integratie met [swagger](https://elysiajs.com/introduction.html)
 
---
# Performance For Loops
*branche 07 for loops*

### start de node versie

```bash
node forloop.js
```

### start de bun versie
```bash
bun start
```
---
# Performance server
express bun en elysia

met [artillery](https://www.artillery.io/docs/get-started/first-test)

ontloopt elkaar niet heel veel

voordelen op openshift?

*toon results* 

---
# Project met Tailwind

*toon crm project*

voordeel alles wordt razend snel door bun gecompileerd

Bun runt project en de bundle 

css wordt gegenereerd door [Tailwind](https://tailwindcss.com/docs/utility-first)

---
# Performance packages en cache

youtube en bun pagina vol met voorbeelden.

---
# Toekomst
Node en Bun zullen voorlopig naast elkaar bestaan 

Bun is nog niet productie klaar 

Geen Windows versie 


---- 
# Bun en Angular 

Installeer new project met ```ng new projectName``` 
daarna cd de map in en  ```bun i```  
De eerste keer duurt dat even lang als npm i.  
```bun start``` om het project te starten. Duurt de eerste keer ook even lang als npm start. 
Als je nu  
```rm package-lock.json && rm -rf /node_modules```  
en daarna weer 
```bun i && bun start``` 
dan gaat alles wel veel sneller (op mijn systeem bunnen 3s ).  
Vooral handig als je snel je node_modules wil verwijderen en weer opnieuw wil installeeren zoals bv bij het upgraden van Angular.  

----
[Github](https://github.com/hubeek/bun01pres)
