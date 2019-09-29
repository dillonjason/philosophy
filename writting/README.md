# Writing Code

This section will provide a process and reasoning for writing any type of code. This means it should work on both backend and frontend applications, as well as UI components such as React.

## Principles

These are the core principles of writing code that will be used as the foundation for the rest of this guide.

### 1. Functions

All code that is not a function call must be written in exported functions that can be executed multiple times.

For example instead of starting node with:

```javascript
const express = require('express');
const app = express();
app.get('/', ...)
...
app.listen(3000)
```

We should create a function `createExpressApp` and use it like:

```javascript
const express = require('express');

function createExpressApp() {
  const app = express();
  app.get('/', ...)
  ...
  return app;
}

const app = createExpressApp();
app.listen(3000);
```

This will ensure that all code is written in small reusable components that can be tested.

### 2. Immutable

Functions should not adjust their parameters or variables out of scope. This includes changing a parameter or variables state.

For example the `createExpressApp` function should **NOT** be written as:

```javascript
function createExpressApp(app) {
  app.get('/', ...)
  ...
  return app;
}

const app = express();
createExpressApp(app)
```

This function manipulates data outside of itself.

### 3. Scoped to self

A function can not access data that is not made available to it via parameters or self instantiation.

#### Violation

```javascript
const a = 1;
const b = 2;

function addWithB(a) {
  return a + b;
}

const sum = addWithB(a);
```

#### Correct

```javascript
const a = 1;
const b = 2;

function add(a, b) {
  return a + b;
}

const sum = add(a, b);
```

### 4. Single Purpose

Every unit of code has a single purpose that it will achieve.
