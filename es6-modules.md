//1) Compare CommonJS (require/module.exports) vs ES6 modules (import/export):
What are the syntax differences?
What are the advantages of ES6 modules?
How do you configure a Node.js project to use ES6 modules?

//Solutions

**Syntax differences:**

*CommonJS:*
```js
// Import
const myModule = require('./myModule');
// Export
module.exports = myFunction;
```

*ES6 Modules:*
```js
// Import
import myModule from './myModule.js';
// Export
export default myFunction;
```

**Advantages of ES6 modules:**
- Native support in modern JavaScript and browsers.
- Static analysis: Imports/exports are known at compile time, enabling better tooling and tree-shaking.
- Cleaner, more concise syntax.
- Supports both named and default exports.

**How to configure Node.js to use ES6 modules:**
1. In your `package.json`, add:
   ```json
   {
     "type": "module"
   }
   ```
2. Use `.js` extension in import paths (e.g., `import x from './file.js'`).
3. Use `import`/`export` syntax instead of `require`/`module.exports`.

*Note:* Some older Node.js features (like `__dirname`) require workarounds in ES6


//2) Explain the different types of exports:
Named exports vs default exports
When would you use each type?
How do you import different types of exports?

//Solution

**Named exports:**  
Allow you to export multiple values (functions, variables, classes) from a module by name.
```js
// Export
export const foo = 1;
export function bar() {}
// Import
import { foo, bar } from './module.js';
```

**Default exports:**  
Allow you to export a single value as the "default" export from a module.
```js
// Export
export default function main() {}
// Import
import main from './module.js';
```

**When to use each:**
- Use **named exports** when you want to export multiple things from a module.
- Use a **default export** when your module only exports one main thing (e.g., a single class or function).

**Importing:**
- Named exports: `import { name } from './module.js';`
- Default export: `import anyName from './module.js';`
- You can combine both:
  ```js
  import main, { foo, bar } from './module.js';
  ```