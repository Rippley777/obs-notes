```
function onlyNumbers(str) {
	return str.replace(/[^0-9]/g, '');
} 

// Example usage
const originalString = "Hello, World! 123";
const numbersOnlyString = onlyNumbers(originalString);
console.log(numbersOnlyString); 

// Outputs: "123"
```