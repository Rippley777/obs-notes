Similar to:
[[Only Numbers ]]

```
function removeNonNumbers(str) {
	return str.replace(/[^\d]/g, '');
} 
// Example usage

const originalString = "Hello, World! 123";
const numbersOnlyString = removeNonNumbers(originalString);
console.log(numbersOnlyString);

// Outputs: "123"
```