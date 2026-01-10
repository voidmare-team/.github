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
- In the start of every sub-header, write a short overview of it:
```c
// ========================================
// Declarations related to arithmetic
// operations. 
// ========================================

#ifndef _VOIDMARE_FOO_MATH_H
#define _VOIDMARE_FOO_MATH_H

// ... 
``` 

### When you write Go code
- Go documentation must follow idiomatic Go principles as described in https://go.dev/doc/comment.
- All packages must have a package comment describing their purpose.
- All exported identifiers must have documentation comments.
- Exported APIs intended for external use must include examples when usage is non-trivial.

## Style code

### When you write C code
- The projects inside `voidmare-team` must use the same `.clang-format`:
```yaml
BasedOnStyle: LLVM
IndentWidth: 2
UseTab: Always
BreakBeforeBraces: Allman
SpaceAfterCStyleCast: false
IndentExternBlock: NoIndent
```
- To make sure your code follows this style, use `clang-format` to format code.

### When you write Go code
- The projects must follow idiomatic Go style principles.
- Use `gofmt` or extensions to make sure your code follows these principles.

## Code writing

### General
- When you write code, always put the following copyright notice at the start of the file:
```c
// Copyright 2026 VOIDMARE Team
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//    http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.
```
- Use the existing tools, which are much stable and safer. Don't try to make your own, unless required.

## Organization

### When you write C code
- All C libraries and tools in `voidmare-team` go into `voidmare/` directory.
- The C code defines two types of headers: **master header** and **sub header**.

#### Master header
- Master header has its own directory with sub-headers.
- Master header must be unique and don't collide with others in `voidmare/` directory.
- Master header represents only one library or tool. 
- Master header includes all its sub-headers inside from its directory.
- Master header must be created inside `voidmare/` directory and always out of its own.
- Example layout:
```
-- voidmare/
-- -- -- foo/
-- -- foo.h
```

#### Sub header
- Sub header covers only one topic-related functionality, which maintains modular and scalable design.
- Sub header can include other sub-headers.
- Sub header must not include the master header to prevent circular depedency.

#### Internal header
- Internal header that are reused across the library go into `<master-header>/internal/` directory.
- Organize functionality in this format: `internal/<scope (may be recursive)>/<header>.h`
- Internal header is considered sub-header, but they're not included in public master header. 

#### Example

- Here's how you can organize them:
```
include/
-- voidmare/
-- -- foo/
-- -- -- math.h
-- -- -- result.h
-- -- foo.h
```

foo.h:
```
#ifndef _VOIDMARE_FOO_H
#define _VOIDMARE_FOO_H

#include "math.h"
#include "result.h"

#endif
```

### When you write Go code
- The projects must follow idiomatic Go code organization principles.
