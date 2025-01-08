```
function lettersAndSpaces(str) {
  return str.replace(/[^a-zA-Z\s]/g, '');
}

// Example usage
const originalString = "Hello, World! 123";
const lettersSpacesString = lettersAndSpaces(originalString);

console.log(lettersSpacesString);  // Outputs: "Hello World "

```