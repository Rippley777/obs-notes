
The `console` API is a powerful tool for debugging and inspecting code. While most developers use basic methods like `console.log`, there are many lesser-known features that can enhance debugging.

---

## Basic Methods

1. console.log - General logging.
   Example: console.log('Logging a message', { key: 'value' })

2. console.error - Highlights errors with a red indicator.
   Example: console.error('This is an error message')

3. console.warn - Highlights warnings with a yellow indicator.
   Example: console.warn('This is a warning message')

4. console.info - Displays informational messages.
   Example: console.info('This is an informational message')

---

## Advanced Methods

### console.table
Displays tabular data in a table format, easier to read than plain objects or arrays.
Example:
const users = [{ id: 1, name: 'Alice' }, { id: 2, name: 'Bob' }]
console.table(users)

You can specify columns:
console.table(users, ['name'])

### console.group and console.groupCollapsed
Organize logs into expandable/collapsible groups.
Example:
console.group('User Details')
console.log('Name: Alice')
console.groupEnd()

### console.time and console.timeEnd
Measure time taken by a block of code.
Example:
console.time('Timer')
for (let i = 0; i < 100000; i++) {}
console.timeEnd('Timer')

### console.trace
Prints a stack trace of the function calls.
Example:
function a() { b() }
function b() { console.trace('Trace log') }
a()

### console.assert
Logs only if the condition is false.
Example:
const isTrue = false
console.assert(isTrue, 'Assertion failed')

### console.clear
Clears the console.

### console.count and console.countReset
Counts how many times a message is logged.
Example:
console.count('Counter')
console.countReset('Counter')

### console.dir
Displays an interactive list of an object's properties.
Example:
const obj = { a: 1, b: { c: 2 } }
console.dir(obj)

---

## Tips and Tricks

- Use console.log with %s, %d, and %c for formatting.
  Example: console.log('%cStyled text', 'color: red; font-size: 20px')
- Use console.profile and console.profileEnd for profiling.
- Use console.dirxml for inspecting DOM elements.

---

## Example Usage

### Debugging API Responses
fetch('/api/data').then(response => response.json()).then(data => {
  console.group('API Data')
  console.table(data)
  console.groupEnd()
})

### Timing Performance
console.time('Render Timer')
renderUI()
console.timeEnd('Render Timer')

---

This guide covers both basic and advanced uses of the console API. With these tools, you can debug more effectively and maintain cleaner logs.
