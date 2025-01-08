O(2^n) = "big O of two to the power of n."

### 1. **O(1) - Constant Time**

Imagine you have a box with only one toy inside. No matter what, you always take just a moment to open the box and get your toy. This is like constant time—no matter how many toys you _could_ have, it always takes the same amount of time to do something.

### 2. **O(n) - Linear Time**

Think of a line of children waiting to get ice cream. If there are 5 kids, each kid gets served one after the other. More kids mean more time to serve everyone. So, if the number of kids doubles, the time doubles. This is linear time; the time it takes grows directly with the number of items (or kids).

### 3. **O(n²) - Quadratic Time**

Suppose each kid in a group needs to high-five every other kid. If there are just 2 kids, that’s only 1 high-five. But with 3 kids, there are 3 high-fives. With 4 kids, there are 6 high-fives, and it keeps growing much faster than the number of kids. This is quadratic time, where the time it takes grows as the square of the number of items.

### 4. **O(2^n) - Exponential Time**

Imagine if every child in a group could split into two more kids every minute, and then those kids could split again, and so on. The number of kids would grow incredibly fast—2, then 4, then 8, then 16, and it keeps doubling very quickly. Algorithms with exponential time complexity also take much more time as the input grows, even a little bit.

### 5. **O(log n) - Logarithmic Time**

This is like the book example I gave you where you keep cutting the problem in half. It’s much faster than having to check every single thing one by one.

### 6. **O(n log n) - Linearithmic Time**

This is a mix between linear and logarithmic. Imagine you had to organize a group of kids into a line from shortest to tallest, but every time you add a kid to the line, you use the fast method of cutting the line in half to find where they should go. It’s faster than making everyone compare heights every time, but not as fast as just counting them.

