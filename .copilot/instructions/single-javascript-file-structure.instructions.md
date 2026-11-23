---
description: "When writing, updating, or refactoring this JavaScript file, you must strictly adhere to the following top-to-bottom structural order. Do not mix code from different sections:"
applyTo: "**/*.js"
---

1. **File Header**: Copyright or project license block comments at the absolute top.
2. **Pragma**: Always declare `'use strict';`.
3. **Imports / Dependencies**: All `require` statements grouped logically (Node.js built-ins, internal database/resource access, shared functions, constants, and then third-party libraries).
4. **Module-level Constants**: Upper-case constants used globally within the file (e.g., pagination limits, batch sizes).
5. **Private Helper Functions**: Functions prefixed with an underscore (`_`) that handle internal logic, data formatting, or validation. Always place these before the main functions that consume them.
6. **Main API / Controller Functions**: The core asynchronous functions that process requests and handle business logic.
7. **Exports block**: A single `module.exports = { ... }` object at the very end of the file, exporting only the public main functions.