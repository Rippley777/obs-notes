
### Simple Split 
```
const splitArray = (arr) => {

	const mid = Math.floor(arr.length / 2);
	
	const left = arr.slice(0, mid);
	
	const right = arr.slice(mid);
	
	return [left, right];

};
```
- **Time Complexity**: O(n), where n is the size of the array, due to slicing.
- **Use Case**: Split the array into two halves.

### Conditional Split

```
const splitArrayByCondition = (arr, conditionFn) => {
  const left = [];
  const right = [];
  for (const item of arr) {
    if (conditionFn(item)) {
      left.push(item);
    } else {
      right.push(item);
    }
  }
  return [left, right];
};
```
- **Time Complexity**: O(n) due to a single loop.
- **Space Complexity**: O(n) for creating two new arrays.
- **Use Case**: Split by a dynamic condition.


### Logical Partition

```
const partition = (arr, conditionFn) => {
  return arr.reduce(
    ([pass, fail], item) => {
      return conditionFn(item)
        ? [[...pass, item], fail]
        : [pass, [...fail, item]];
    },
    [[], []]
  );
};
```

- **Time Complexity**: O(n).
- **Space Complexity**: Higher due to array spread (`...`) in each iteration.
- **Use Case**: Functional programming style.


### In-Place Partition (Optimized Space)

```
const partitionInPlace = (arr, conditionFn) => {
  const left = [];
  const right = [];
  for (const item of arr) {
    (conditionFn(item) ? left : right).push(item);
  }
  return [left, right];
};

const arr = [1, 2, 3, 4, 5, 6];
const [evens, odds] = partitionInPlace(arr, (x) => x % 2 === 0);
console.log(evens); // [2, 4, 6]
console.log(odds);  // [1, 3, 5]

```
- **Time Complexity**: O(n).
- **Space Complexity**: O(n), but avoids multiple intermediate arrays.
- **Use Case**: Minimize space and intermediate steps.
### Key Notes:

- **Avoiding Mutations**: If immutability is important, prefer `slice` or `reduce`.
- **Performance**: Use a single loop approach for the best performance.
- **Custom Conditions**: For splitting based on custom logic, use approaches that allow flexible `conditionFn`.