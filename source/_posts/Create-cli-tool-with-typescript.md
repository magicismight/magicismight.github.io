---
layout: title
title: Create cli tool with typescript
date: 2021-08-11 22:17:36
tags:
---

# Create cli tool with typescript.

1. Specify a JavaScript file for 'bin' in package.json

``` JSON
"name": "some-cli-tool-name",
"bin": {
  "some-cli-tool-name": "./bin.js"
},
```

2. Create `./bin.js`

``` js
#!/usr/bin/env node

// Register `ts-node` into node.js environment with a project option,
// cli will throw `Cannot use import statement outside a module ts-node` if `project` not is not found.
require('ts-node').register({
  project: require('path').join(__dirname, './tsconfig.json')
});

// Run cli
require('./src/index.ts');

```

1. Add `shebang` for node at the top of `./src/index.ts`, 

```ts
#!/usr/bin/env ts-node

const message: string = 'It works!';
console.log(message);
```

4. Create `tsconfig.json` and fill with configuration.

5. Write your cli tool with typescript.

6. Publish to npm.

7. Done.

Using npx to run the cli tool you just write in typescript.
`npx some-cli-tool-name`

# NOTICE:

ALL TYPESCRIPT DEPENDENCIES MUST ADD TO `"dependencies"` IN `package.json` . LIKE: `typescript` ITSELF AND `@types/*` TYPE DEFINITIONS.

