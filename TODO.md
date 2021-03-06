# Latte-lang TODOs

## Modularization /2016-10-23

latte-compiler can be divided into 4 parts:

* latte-compiler-scanner-parser takes string input and produce AST
* latte-compiler-semantic takes AST and produce bytecode-like semantic objects
* latte-compiler-code-gen produce bytecode
* latte-compiler contains Latte lang, repl and other runtime necessary dependencies

## Value Available Assurance /2016-10-16

Some language support `null safety` (e.g. Kotlin). Latte would support a better value assurance. However, when calling a java method, there's no guarantee that the result would be safe. So Latte don't provide checking for methods outside, only checking inside the method.

When defining a method, let each param be `null safe` or `value available` or `no assurance` as default.

* ~~add new modifier for variables (`notnull`, `notempty`. The first only checks null/Unit, the second cast the value to bool can check the result).~~ / 2016-10-18 **DONE**
* ~~implement the modifiers for params and return values~~ / 2016-10-18 **DONE**
* ~~implement the modifiers for local variables~~ / 2016-10-22 **DONE**
* ~~implement the modifiers for fields~~ /2016-10-18 **REMOVED**

## Performance and Accuracy 1 /2016-10-15

There are multiple things can be refactored, especially the lambda expression.
First step would be these tasks:

* ~~`val` variable types can be predicted. (EASY)~~ / 2016-10-16 **DONE**
* ~~when generating lambda expression, non-accessible variables (those with an invalid name) can be ignored. (HARD)~~ / 2016-10-23 **DONE**
* scanner can be refactored. (HARD)
* ~~step 1 should be refactored. first retrieve all packages that's defined in source code, then check import. (MEDIUM)~~ / 2016-10-16 **DONE**
* ~~scan class path to see whether a package exist. (EASY)~~ / 2016-10-16 **DONE**

## Full Function Support /2016-10-14

The current `function type` support is not good enough. Any thing that is invokable should be seen as a function.

Here's the what to do:

* ~~remove inner method, replace with lambda (EASY)~~ /2016-10-16 **REMOVE** methods are methods, they divide from functions

  a method can be directly accessed without `(...)` to have it invoked, but a function is passed as a variable.
  they are not the same

* ~~use `fun` as modifier when defining methods (just like kotlin) (EASY)~~ /2016-10-16 **DONE** but instead of `fun`, we use `def`

  the functions shoud be considered differently from methods.  
  and now statements like `def m=1` can be used. `def m=1`,`def m:int=1`,`def m:int |- ...`,`def m:int`,`def m |- ...`,`def m`

* ~~constructor as a function, when calling the function, a new object would be returned (MEDIUM)~~ **REMOVE**
* ~~method as a function, when calling the function, the method would be invoked (MEDIUM)~~ **REMOVE**
* bind argument to function, which generates a new function (HARD)
