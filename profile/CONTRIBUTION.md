# Contribution 

First of all, we appreciate your help and are very thankful for your time.
The contribution guidelines are required to make sure everyone use the same code style, documentation style etc.

You're always welcome to contribute and suggest improvements to our tools, libraries and projects.

## Documentation

### When you write C code
- Write documentation as short as possible, but still keep it informative and consistent.
- If you need to write special notes, write it in `Notes` section:
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
- Write about errors the function returns in some cases:
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
