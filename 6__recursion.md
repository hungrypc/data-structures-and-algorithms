# recursion

## the call stack

when functions are invoked, there's a built in data structure that manages what happens - this is called the **call stack**

- it's a **stack** data structure
- any time a function is invoked, it's places (pushed) on the top of the call stack
- when javascript see's the **return** keyword OR when the function ends, the compiler will remove (pop) the top item of the stack

when we write recursive functions, we keep pushing new functions onto the call stack

## how recursive functions work

invoke the same function with a different input until you reach your **base case**

base case:
- the condition when the recursion ends

