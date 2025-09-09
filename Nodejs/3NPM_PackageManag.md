# NPM & Package Management

NPM (**Node Package Manager**) is used to manage JavaScript packages and libraries for Node.js projects.

---

## 1. Installing and Using Packages

### Install a package
```bash
npm install package-name
```
#### Example:
```js

npm install express

```

Using the package

```js

const express = require("express");
const app = express();

app.get("/", (req, res) => {
    res.send("Hello from Express!");
});

app.listen(3000, () => console.log("Server running on port 3000"));

```

## 2. package.json and Its Importance

    A configuration file for any Node.js project.

### Stores:

- Project name & version

- Dependencies

- Scripts

- Metadata

 Create package.json:

 ```js

 {
  "name": "my-app",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}

```


## 3. devDependencies vs dependencies
Type	Command	                        Usage
- dependencies	npm install package	 Required for production
- devDependencies	npm install package --save-dev	-  Required for development only

### Example:

```js 

npm install nodemon --save-dev
```

## 4. Versioning in NPM

```bash
^ (Caret) → Updates minor and patch versions
Example: ^1.2.3 → updates to 1.x.x but not 2.x.x

~ (Tilde) → Updates only patch versions
Example: ~1.2.3 → updates to 1.2.x but not 1.3.x

Exact Version → Install exact version
Example: 1.2.3 → stays on 1.2.3

```

## 5. Using npx

- npx runs Node.js packages without installing them globally.

### Example:

```js

npx create-react-app myapp

```

This directly runs create-react-app without needing global install.


## Summary Table
- Command/Concept	Description
- npm install	Install packages
- package.json	Project metadata & dependencies
- devDependencies	Dev tools (e.g., nodemon, eslint)
- dependencies	Required for production
- ^version	Minor + patch updates allowed
- ~version	Only patch updates allowed
- npx	Execute packages without global install