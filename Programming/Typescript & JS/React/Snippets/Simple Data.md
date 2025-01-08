
## Omit
```
const omit = (obj, keysToOmit) => Object.fromEntries( Object.entries(obj) .filter(([key]) => !keysToOmit.includes(key)) );
```

This version of the `omit` function works as follows:

- `Object.entries(obj)` converts the object into an array of `[key, value]` pairs.
- `.filter(([key]) => !keysToOmit.includes(key))` filters out the entries whose keys are in the `keysToOmit` array.
- `Object.fromEntries()` converts the filtered array of key-value pairs back into an object.