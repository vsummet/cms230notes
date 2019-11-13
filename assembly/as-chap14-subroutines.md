# Chapter 14: Subroutines in ARM Assembly

All high level languages have the concept of a **subroutine** (sometimes called procedure, function, or method). A subroutine is a logical division of the code that may be regarded as a self-contained operation. For example, the `power` function is usually implemented as a subroutine.

This chapter looks at a simple implementation in assembly language of this idea. The simple implementation is not adequate for the full power of subroutines (as implemented in high level languages), but is a good starting point. It corresponds to the type of subroutines implemented in the early days of programming.

Chapter Topics:
* Subroutine call
* Caller and Callee routines
* `bl` instruction
* The $ra register
* The simple linkage calling convention
* Register use in subroutines


