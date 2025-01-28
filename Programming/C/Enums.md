```c
typedef enum DaysOfWeek {
  MONDAY,
  TACO_TUESDAY,
  WEDNESDAY,
  THURSDAY,
  FRIDAY,
  SATURDAY,
  FUNDAY,
} days_of_week_t;
```
```c
typedef struct Event {
  char *title;
  days_of_week_t day;
} event_t;

// Or if you don't want to use the alias:

typedef struct Event {
  char *title;
  enum DaysOfWeek day;
} event_t;
```

#### defaults
```c
typedef enum {
  EXIT_SUCCESS = 0,
  EXIT_FAILURE = 1,
  EXIT_COMMAND_NOT_FOUND = 127,
} ExitStatus;
```

### switch case


One of the best features of `enums` is that it can be used in [`switch` statements](https://en.cppreference.com/w/c/language/switch). Enums + switch statements:

- Avoid "[magic numbers](https://en.wikipedia.org/wiki/Magic_number_(programming))"
- Use descriptive names
- With modern tooling, will give you an error/warning that you haven't handled all the cases in your switch


```c
switch (logLevel) {
  case LOG_DEBUG:
    printf("Debug logging enabled\n");
    break;
  case LOG_INFO:
    printf("Info logging enabled\n");
    break;
  case LOG_WARN:
    printf("Warning logging enabled\n");
    break;
  case LOG_ERROR:
    printf("Error logging enabled\n");
    break;
  default:
    printf("Unknown log level: %d\n", logLevel);
    break;
}
```



```c
#include <stdio.h>

typedef enum {
  BIG = 123412341234,
  BIGGER,
  BIGGEST,
} BigNumbers;

typedef enum {
  HTTP_BAD_REQUEST = 400,
  HTTP_UNAUTHORIZED = 401,
  HTTP_NOT_FOUND = 404,
  HTTP_I_AM_A_TEAPOT = 418,
  HTTP_INTERNAL_SERVER_ERROR = 500
} HttpErrorCode;

int main() {
  // ?


  printf("The size of BigNumbers is %zu bytes\n", sizeof(BigNumbers));
  printf("The size of HttpErrorCode is %zu bytes\n", sizeof(HttpErrorCode));
  return 0;
}

```
```c
typedef union SnekObjectKind {
  INTEGER,
  STRING,
} snek_object_kind_t;

```

```c
void format_object(snek_object_t obj, char *buffer) {
  switch (obj.kind) {
    case INTEGER:
    sprintf(buffer, "int:%d", obj.data.v_int);
    break;
    case STRING:
      sprintf(buffer, "string:%s", obj.data.v_string);
      break;
  }
}
```