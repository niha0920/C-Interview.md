## Why is C called a mid-level programming language?
C is called a mid-level language because:
- It supports both low-level hardware manipulation and high-level programming abstractions.
- It is suitable for system-level tasks like operating systems and for application-level development.
- It provides a balance between performance, control, and portability, making it versatile for both hardware and software interfaces.

## What are the features of the C language?
- The features that make C powerful and enduring include simplicity, modularity, portability, memory management, and speed.
- Its balanced nature between hardware-level control and software-level abstraction makes it one of the most influential programming languages in computing history

## What is a token?
- A token is the fundamental building block of a program that helps the compiler understand and translate the source code. 
- In essence, every word, number, operator, or symbol that has meaning to the compiler is considered a token.

## What is the use of printf() and scanf() functions? Also explain format specifiers? 
- printf() is used for displaying output.
- scanf() is used for taking input.
- Format specifiers define the type and format of data for input and output, ensuring correct handling of variables.

## What's the value of the expression 5["abxdef"]?
The value of 5["abxdef"] is the character 'f' in C.

## What is a built-in function in C?
- A built-in function in C is a ready-to-use function defined in the C standard libraries providing essential functionalities.
- Leveraging these functions helps write efficient and portable code by reusing well-tested routines instead of writing code from scratch.

## What is a Preprocessor?
- The preprocessor is an essential first phase in the C compilation process.
- By handling file inclusion, macro substitution, and conditional compilation before actual compilation, it enables flexible, maintainable, and efficient source code management.

## In C, What is the #line used for?
- The #line directive is mainly used for debugging and error reporting enhancement.
- It helps in mapping the compiled code back to its original source or logical sections, especially in situations involving code generation or macro expansion, aiding developers in effective troubleshooting.

## How can a string be converted to a number?
- To convert a string to a number in C, common functions are atoi() (simple), strtol() (safer, more control), and sscanf() (formatted input parsing).
- Manual conversions are also possible but more error-prone.
- Choosing the method depends on the required robustness and error handling.

## How can a number be converted to a string
- The most common and portable way to convert a number to a string in C is with sprintf() by specifying appropriate format specifiers.
- This allows converting integers, floats, and other number types conveniently and storing them as strings for further use.

## What is recursion in C?
- Recursion in C enables elegant solutions for problems that can be defined in terms of smaller instances of themselves.
- It consists of recursive calls progressing toward a base case and is a core concept used in algorithms, mathematical computations, and data structure operations like tree and graph traversal.

## Why doesn’t C support function overloading?
C doesn’t support function overloading because:
- Its compiler does not perform name mangling.
- It only differentiates functions by name, not by argument type or number.
- It was designed as a procedural language, not for object-oriented features like polymorphism.​

## What is the difference between global int and static int declaration?
- A global int is accessible throughout the entire program and across multiple files, exhibiting external linkage.
- A static int declared globally has its scope limited to the defining file (internal linkage), preventing access from other files. When declared inside a function, it maintains its value between function calls but remains local to that function.
- Both have the same lifetime (during program execution) but differ in their visibility and scope.

## What is a pointer in C?
A pointer is a special variable in C that stores and manipulates the address of another variable, enabling direct memory access and efficient programming techniques essential for system-level and embedded programming.

## Difference between const char* p and char const* p?
| Declaration          |  Meaning                                     |
| -------------------- | -------------------------------------------- |
| const char *p        |  Pointer to constant char (data is const)    |
| char const *p        |  Same as above                               |
| char *const p        |  Constant pointer to char (pointer is const) |
| const char *const p  |  Constant pointer to constant char           |
- Thus, const char* p and char const* p are interchangeable and mean the same thing.

## What is pointer to pointer in C?
- A pointer to pointer in C is a variable that stores the address of another pointer, allowing multiple levels of indirection to access or modify data.
- This concept is widely used for dynamic data structures and advanced memory handling.

## Why n++ executes faster than n+1 ?
- In theory and low-level CPU instructions, n++ (increment) is faster than n = n + 1 (add and assign) because it is a simpler, atomic operation.
- In practice, modern compilers optimize both into the same machine code, making their execution speed effectively identical.
- The choice should be based on clarity and intent rather than speed in typical modern programming environments.

## What is typecasting in C?
- Typecasting in C is a way to explicitly convert one data type into another to control how data is interpreted and manipulated during program execution.
- It is an essential tool for precise type handling and accurate operations in C programming.

## What are the advantages of Macro over function?
- Macros offer speed and flexibility advantages for small, repeated code snippets or platform-dependent code.
- However, they lack type safety and can increase code size, so functions are preferred for maintainability and debugging except in specific performance-critical or generic scenarios.

## What are Enumerations?
Enumerations in C are a powerful way to create a set of named integer constants, improving code clarity, reducing errors, and aiding maintainability by replacing numeric literals with descriptive names.

## When should we use the register storage specifier?
- You should use the register storage specifier to hint the compiler to store frequently accessed local variables in CPU registers to improve execution speed.
- However, modern compilers optimize automatically, and the register keyword is often ignored today.

## Specify different types of decision control statements?
| Statement Type | Purpose                                       |
| -------------- | --------------------------------------------- |
| if             | Executes code block if condition is true      |
| if-else        | Executes code block for true/false conditions |
| nested if      | Handles multiple, nested conditions           |
| else-if ladder | Checks multiple conditions in sequence        | 
| switch         | Selects block based on variable’s value       |
- These statements help control the logical flow of a program by allowing choices based on conditions.

## What is an r-value and l-value?
- l-value: Has a memory address, can be assigned to.
- r-value: Does not have a memory address, represents a value, cannot be assigned to.

## What is the difference between malloc() and calloc()?
| Feature        | malloc()                       | calloc()                             |
| -------------- | ------------------------------ | ------------------------------------ |
| Initialization | No (memory has garbage values) | Yes (memory set to zero)             |
| Arguments      | One (total bytes)              | Two (num elements, size of each)     |
| Speed          | Faster                         | Slower                               |
| Syntax         | void *malloc(size_t size);     | void *calloc(size_t n, size_t size); |
- Both functions return a pointer to the allocated memory block or NULL if allocation fails.

## What is the difference between struct and union in C?
- Structure: Use when you want to store and use multiple member values at the same time.
- Union: Use when you need only one member at a time, saving memory by storing different data types in the same location.

## What is call by reference in functions?
Call by reference allows passing variables to functions by their address, enabling the function to modify the original variables directly rather than working with copies, thus providing efficient and flexible parameter passing.

## What is pass by reference in functions?


## What is a memory leak? How to avoid it?

## What is Dynamic memory allocation in C? Name the dynamic allocation functions.

## What is typedef?

## Why is it usually a bad idea to use gets()? Suggest a workaround.
