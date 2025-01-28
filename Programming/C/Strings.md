
<string.h> header functions

## `strcpy` - copy string
```c
char src[] = "Hello";
char dest[6];
strcpy(dest, src);
// dest now contains "Hello"
```

## `strcat` - concat string
```c
char dest[12] = "Hello";
char src[] = " World";
strcat(dest, src);
// dest now contains "Hello World"
```

## `strlen` - get string length
```c
char str[] = "Hello";
size_t len = strlen(str);
// len is 5
```

## `strcmp` - lexicographical comparison 
```c
char str1[] = "Hello";
char str2[] = "World";
int result = strcmp(str1, str2);
// result is negative since "Hello" < "World"
```

## `strcpy` - copy # of chars to other str
```c
char src[] = "Hello";
char dest[6];
strncpy(dest, src, 3);
// dest now contains "Hel"
dest[3] = '\0';
// ensure null termination
```

## `strncat` - concats # of chars to other str
```c
char dest[12] = "Hello";
char src[] = " World";
strncat(dest, src, 3);
// dest now contains "Hello Wo"
```

## `strchr` - find 1st occurrence of char in str
```c
char str[] = "Hello";
char *pos = strchr(str, 'l');
// pos points to the first 'l' in "Hello"
```

## `strstr` - find 1st occurrence of substring in str
```c
char str[] = "Hello World";
char *pos = strstr(str, "World");
// pos points to "World" in "Hello World"
```
# Danger

```

void concat_strings(char *str1, const char *str2) {
  char *end = str1;
  while (*end != '\0') {
    end++;
  }

  while (*str2 != '\0') {
    *end = *str2;
    *end++;
    *str2++;
  }
}

```

```c
char str1[5] = "cat"; // Only space for 5 chars
char *str2 = "elephant"; // Trying to add 8 chars
```

This would write past the end of `str1`'s allocated memory, which could:

1. Corrupt other variables in memory
2. Crash the program
3. Create security vulnerabilities (this is how many hackers exploit programs!)

That's why in real C code, you'd typically:

- Use safer functions like `strlcat`
- Check buffer sizes before concatenating
- Use string length limits
- Or use more modern string libraries


```c
const int max_buffer_size = 64;
size_t available_space = max_buffer_size - dest->length - 1;  // -1 for null terminator
```



```c
#include <string.h>
#include "exercise.h"

int smart_append(TextBuffer* dest, const char* src) {
  if (!dest || !src) {
    return 1;
  }

  const int max_buffer_size = 64;
  size_t src_len = strlen(src);
  size_t available_space = max_buffer_size - dest->length - 1;
  if (src_len > available_space) {
    strncat(dest->buffer, src, available_space);
    dest->length = max_buffer_size - 1;
    return 1;
  }
  strcat(dest->buffer, src);
  dest->length += src_len;
  return 0;
  
}

```