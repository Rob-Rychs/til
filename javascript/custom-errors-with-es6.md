# Custom errors with ES6

You can easily create custom errors by extend the native error with ES6. Extend from the following to get custom errors with useful stacktrace.

```javascript
class ExtendableError extends Error {
  constructor(message) {
    super(message)
    this.name = this.constructor.name

    if (typeof Error.captureStackTrace === 'function') {
      Error.captureStackTrace(this, this.constructor)
    } else {
      this.stack = new Error(message).stack
    }
  }
}

export default ExtendableError
```

If you use Babel you need to add `babel-plugin-transform-builtin-extend`.

```
{
  "plugins": [
    ["babel-plugin-transform-builtin-extend", {
      "globals": ["Error"]
    }]
  ]
}
```