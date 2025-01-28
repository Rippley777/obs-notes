```
void coordinate_update_x(coordinate_t* coord, int new_x) {
    coord->x = new_x;  // Notice the -> operator for accessing through a pointer
}
```

```
coordinate_t c = {1, 2, 3};
coordinate_update_x(&c, 4);  // Pass the address of c
```


## Diagram Explanation

Let's assume `numbers` is stored starting at memory address `0x1000`. An integer is typically 4 bytes in C. Here's how the array elements are laid out in memory:

|Address|Element|Value|
|---|---|---|
|0x1000|numbers[0]|1|
|0x1004|numbers[1]|2|
|0x1008|numbers[2]|3|
|0x100C|numbers[3]|4|
|0x1010|numbers[4]|5|

## Accessing Elements Using Pointers

- `numbers + 0` or `&numbers[0]` points to `0x1000`
- `numbers + 1` or `&numbers[1]` points to `0x1004`
- `numbers + 2` or `&numbers[2]` points to `0x1008`
- `numbers + 3` or `&numbers[3]` points to `0x100C`
- `numbers + 4` or `&numbers[4]` points to `0x1010`

## Example Code

```c
#include <stdio.h>

int main() {
  int numbers[5] = {1, 2, 3, 4, 5};

  // Accessing elements using array indexing
  printf("numbers[2] = %d\n", numbers[2]);  // Output: 3

  // Accessing elements using pointers
  printf("*(numbers + 2) = %d\n", *(numbers + 2));  // Output: 3

  // Pointer arithmetic
  int *ptr = numbers;
  printf("Pointer ptr points to numbers[0]: %d\n", *ptr);  // Output: 1
  ptr += 2;
  printf("Pointer ptr points to numbers[2]: %d\n", *ptr);  // Output: 3

  return 0;
}
```


## Memory Layout

Assuming each `int` is 4 bytes, the `Coordinate` structure will be 12 bytes (`3 * 4` bytes). Let's assume the `points` array starts at memory address `0x2000`.

Here is the memory layout:

|Address|Element|Value|Offset (bytes)|
|---|---|---|---|
|`0x2000`|`points[0].x`|1|0|
|`0x2004`|`points[0].y`|2|4|
|`0x2008`|`points[0].z`|3|8|
|`0x200C`|`points[1].x`|4|12|
|`0x2010`|`points[1].y`|5|16|
|`0x2014`|`points[1].z`|6|20|
|`0x2018`|`points[2].x`|7|24|
|`0x201C`|`points[2].y`|8|28|
|`0x2020`|`points[2].z`|9|32|

## Accessing Elements Using Pointers

- `points + 0` or `&points[0]` points to `0x2000`
- `points + 1` or `&points[1]` points to `0x200C` (next structure, offset by 12 bytes)
- `points + 2` or `&points[2]` points to `0x2018`


# Arrays Decay to Pointers