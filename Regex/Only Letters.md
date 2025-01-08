```
function onlyLetters(str) {
	return str.replace(/[^a-zA-Z]/g, '');
} 

// Example usage
const originalString = "Hello, World! 123";
const lettersOnlyString = onlyLetters(originalString);
console.log(lettersOnlyString);

// Outputs: "HelloWorld"
```