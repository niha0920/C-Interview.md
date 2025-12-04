## 1. Storage classes
| Keyword    | Meaning                        | Lifetime | Scope        | Example                 |
| ---------- | ------------------------------ | -------- | ------------ | ----------------------- |
| `auto`     | Default for local vars         | Block    | Local        | `auto int a = 5;`       |
| `static`   | Persists across function calls | Program  | Local/Global | `static int count = 0;` |
| `extern`   | Declared in another file       | Program  | Global       | `extern int x;`         |
| `register` | Suggests CPU register use      | Block    | Local        | `register int i;`       |
### Q: What’s the difference between static and extern variables?
Static limits visibility within the file; extern extends visibility across files.
## 2. Pointers & Arrays
A pointer stores an address.
```c
int a = 10;
int *p = &a;
printf("%d", *p);   // 10
```
Array name = address of its first element.
- `arr[i] == *(arr + i)`
### Q:
```c
int a[5] = {1,2,3,4,5};
int *p = a;
printf("%d %d", *(p+2), 2[p]);
```
Output: `3 3` (since `2[p] == *(p+2)`).
## 3. Dynamic Memory Allocation
- malloc() – allocates uninitialized memory.
- calloc() – allocates & initializes to 0.
- realloc() – resizes a block.
- free() – releases memory.
forgetting to free() → memory leak.
### Q: What happens if you free the same pointer twice?
Undefined behavior (often segmentation fault).
## 4. Structures & Unions
```c
struct emp {
    int id;
    char name[20];
};
```
- Structures → all members have own memory.
- Unions → all members share the same memory.
### Q: Size of union with int, float, char[10]?
10 bytes (max of its members).
## 5. Const and Volatile
- const → variable cannot be modified.
- volatile → tells compiler that the value can change anytime (used for HW registers).
```c
volatile int *status_reg = (int*)0x4000;
```
Define a pointer status_reg that points to the hardware register located at address 0x4000, and make sure all reads and write to it are done exactly as written (no compiler optimizations).
- status_reg is a pointer to a volatile integer.
- Every time ypu read *status_reg, it will actually access hardware memory (not a cached value).
- Every time you write to *status_reg, the compiler ensures a real write occurs.
### Example
```c
#include <stdio.h>
volatile int *status_reg = (int*)0x4000;
int main() {
    int value = *status_reg;   // Read from hardware register
    *status_reg = 0x01;        // Write 0x01 to hardware register
    return 0;
}
```
### Q: Why use volatile in embedded code?
To prevent compiler optimization when the variable is modified by hardware / ISR.
## 6. Function Pointers
```c
int add(int a,int b){return a+b;}
int (*fptr)(int,int) = add;
printf("%d", fptr(3,4));
```
Useful for callbacks, drivers, and state machines.
## Program 1 — Dynamic 2D Array
```c
#include<stdio.h>
#include<stdlib.h>
int main()
{
 int row = 3, col = 4;
 int **arr = malloc(row * sizeof(int*));
 for(int i = 0; i < row; i++)
 {
  arr[i] = malloc(col * sizeof(int));
 }
 for(int i = 0; i < row; i++)
 {
  for(int j = 0; j < col; j++)
  {
   arr[i][j] = i + j;
  }
 }
 for(int i = 0; i < row; i++)
 {
  for(int j = 0; j < col; j++)
  {
   printf("%d ", arr[i][j]);
  }
  printf("\n");
 }
 for(int i = 0; i < row; i++)
 {
  free(arr[i]);
 }
 free(arr);
}
```
## Program 2 — Custom `strlen()`
```c
#include<stdio.h>
int my_strlen(const char *s)
{
 int len = 0;
 while(*s++)
 {
  len++;
 }
 return len;
}
int main()
{
 char s[100];
 scanf("%s", s);
 int result = my_strlen(s);
 printf("%d", result);
}
```
## Program 3 — Function Pointer Callback
```c
#include<stdio.h>
void greet()
{
 printf("Hello from callback");
}
void caller(void (*f)())
{
 f();
}
int main()
{
 caller(greet);
}
```
## 1. What is a dangling pointer?
A dangling pointer is a pointer that points to a memory location which has been freed or is no longer valid.
```c
int *p = malloc(sizeof(int));
*p = 10;
free(p);    // Memory released
printf("%d", *p);  // ❌ Dangling pointer (undefined behavior)
```
#### fix
```c
free(p);
p = NULL;   // Good practice — avoids accidental use
```
## 2. Difference between stack and heap memory?
| Feature             | **Stack**                                                       | **Heap**                               |
| ------------------- | --------------------------------------------------------------- | -------------------------------------- |
| **Allocation type** | Automatic                                                       | Manual (`malloc`, `calloc`, `free`)    |
| **Lifetime**        | Created/destroyed automatically when function is called/returns | Stays allocated until freed explicitly |
| **Speed**           | Very fast                                                       | Slower (requires system calls)         |
| **Size limit**      | Usually small (few MBs)                                         | Large (depends on RAM)                 |
| **Management**      | Managed by compiler                                             | Managed by programmer                  |
| **Example**         | `int x = 10;`                                                   | `int *p = malloc(sizeof(int));`        |
- Memory leaks happen in heap, not in stack.
## 3. Explain pointer-to-const vs const pointer.
### (a) Pointer to const
```c
const int *p;
```
- You cannot modify the value being pointed to (`*p`),
- but you can change where it points.
#### Example:
```c
const int a = 10, b = 20;
const int *p = &a;
p = &b;       // ✅ OK
//*p = 30;    // ❌ Error — can't modify value
```
### (b) Const pointer
```c 
int *const p;
```
- You can modify the value pointed to,
- but cannot change the pointer’s address.
#### Example:
```c
int a = 10, b = 20;
int *const p = &a;
*p = 30;    // ✅ OK
//p = &b;   // ❌ Error — pointer is constant
```
### (c) Const pointer to const
```c
const int *const p = &a;
```
Neither pointer nor value can be modified.
## 4. What are the 4 types of storage classes?
| Storage Class | Keyword    | Memory Location             | Default Value | Scope        | Lifetime       |
| ------------- | ---------- | --------------------------- | ------------- | ------------ | -------------- |
| **Automatic** | `auto`     | Stack                       | Garbage       | Block        | Function ends  |
| **Register**  | `register` | CPU register (if available) | Garbage       | Block        | Function ends  |
| **Static**    | `static`   | Data segment                | Zero          | Block/Global | Entire program |
| **External**  | `extern`   | Data segment                | Zero          | Global       | Entire program |
#### Example:
```c
auto int a = 10;        // local variable (default)
register int i = 0;     // stored in CPU register (maybe)
static int count = 0;   // retains value between calls
extern int globalVar;   // defined in another file
```
## 5. How is memory allocated for a 2D array dynamically?
### Array of pointers
```c
int rows = 3, cols = 4;
int **arr = malloc(rows * sizeof(int*));
for (int i = 0; i < rows; i++)
    arr[i] = malloc(cols * sizeof(int));
```
#### To access:
```c
arr[i][j] = i + j;
```
#### To free:
```c
for (int i = 0; i < rows; i++)
    free(arr[i]);
free(arr);
```
## 6. What’s the size of struct {char a; int b;} on a 32-bit system? (→ 8 bytes due to padding)
```c
struct sample {
    char a;
    int b;
};
```
### Memory layout
| Member      | Size    | Offset |
| ----------- | ------- | ------ |
| `a`         | 1 byte  | 0      |
| **Padding** | 3 bytes | 1–3    |
| `b`         | 4 bytes | 4–7    |
- Total = 8 bytes
#### Reason:
To maintain alignment, compiler inserts padding bytes so that each `int` starts at a multiple of 4 bytes (on 32-bit systems).
```c
#include <stdio.h>
struct sample { char a; int b; };

int main() {
    printf("Size = %zu\n", sizeof(struct sample));
    return 0;
}
```
