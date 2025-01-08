### **Summary of Key Differences**

|**Option**|**`tsconfig.app.json` (Client)**|**`tsconfig.node.json` (Server)**|
|---|---|---|
|`jsx`|`"react"`|_Not needed_|
|`declaration`|_Not needed_|`true`|
|`declarationDir`|_Not needed_|`./dist/types`|
|`emitDeclarationOnly`|_Not needed_|`true`|
|`outDir`|Optional|Mandatory|
|`target`|`ES5` (browser compatibility)|`ES5` or higher (depending on Node.js version)|

---

### **Why the Split?**

- `jsx` is only needed for React or client-side projects.
- `declaration` and related options are generally used for library development or generating reusable type definitions, common in server-side setups or package development.