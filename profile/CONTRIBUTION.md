# Contribution 

First of all, we appreciate your help and are very thankful for your time.
The contribution guidelines are required to make sure everyone use the same code style, documentation style etc.

You're always welcome to contribute and suggest improvements to our tools, libraries and projects.

## Documentation

### When you write C code
- Write documentation as short as possible, but still keep it informative and consistent.
- All below rules are related to structures, types, functions and variables.
- If you need to write special notes, or you need to tell about non-obvious behavior, write it in `Notes` section.
```c
// Adds two numbers and returns the result.
//
// Notes:
// - The function may allocate dynamic array if the result is higher than 100.
int add(int x, int y) {
  int result = x + y;
  if (result > 100) {
    int *new_ptr = (int *)malloc(5 * sizeof(int)):
    // do something with it
  }
  // ...
}
```
- Write about errors the function returns in some cases in `Error codes`.  Don't document about `err_ok` or something simillar, this error code is already telling us everything is okay:
```c
// Divides a by b.
//
// Error codes:
// - err_division_by_zero: If b is zero.
err_t add(int a, int b) {
  if (b == 0) {
     return err_division_by_zero;
  }
  int result = a / b;
  return err_ok;
}
```
- Write about the parameters in `Parameters`:
```c
// Prints number into console.
//
// Parameters:
// - num: Number to print.
void print(int num) {
  printf("%d", num);
}
```
- In total:
```c

// Represents the dynamic array, which is safer and faster
// to use.
typedef struct slice [
  char *data;
  size_t size;
  size_t capacity;
} slice_t;  

// Initializes a pointer to slice_t.
//
// Parameters:
// - slice: A pointer to initialize.
// - initial_cap: Initial capacity.
//
// Notes:
// - initial_cap only allocates memory; it does NOT initialize elements.
err_t slice_init(slice_t *slice, size_t initial_cap);

```

### When you write Go code
- Go documentation must follow idiomatic Go principles as described in https://go.dev/doc/comment.
- All packages must have a package comment describing their purpose.
- All exported identifiers must have documentation comments.
- Exported APIs intended for external use must include examples when usage is non-trivial.
