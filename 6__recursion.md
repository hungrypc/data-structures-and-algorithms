# recursion

## the call stack

when functions are invoked, there's a built in data structure that manages what happens - this is called the **call stack**

- it's a **stack** data structure
- any time a function is invoked, it's places (pushed) on the top of the call stack
- when javascript see's the **return** keyword OR when the function ends, the compiler will remove (pop) the top item of the stack

when we write recursive functions, we keep pushing new functions onto the call stack

## how recursive functions work

invoke the same function with a **different input** until you reach your **base case**

base case:
- the condition when the recursion ends

simple example:
```js
function countDown(num) {
  if (num <= 0) {             // basecase
    console.log("All done!");
    return;
  }
  console.log(num);
  num --;
  countDown(num);             // invokes itself with new input
}
```

another example:
```js
function sumRange(num) {
  if (num === 1) return 1;        // basecase
  return num + sumRange(num - 1); // invoke
}
```

 factorial example:
```js
function factorial(num) {
  if (num === 1) return 1;
  return num * factorial(num - 1);
}
```

## common pitfalls

- no base case
  - causes an infinite loop
- forgetting to return or returning the wrong thing
  - can also cause an infinite loop
- stack overflow
  - too many things in the stack (maximum call stack size exceeded)


## helper method recursion

so far, everything we've written are single standalone functions that calls itself. with helper method recursion, we have two functions - an main outer function, and a recursive function inside the outer function

this is commonly done when we need to compile

eg. collect all of the odd values in an array
```js
function collectOddValues(arr) {
  let result = [];

  function helper(helperInput) {
    if (helperInput.length === 0) {
      return;
    }

    if (helperInput[0] % 2 !== 0) {
      result.push(helperInput[0]);
    }

    helper(helperInput.slice(1));
  }

  helper(arr);

  return result;
}
```

so the reason we do this is because the outer function needs to be there to initialize and manipulate result

BUT, we can still do this without this helper method structure, albeit a little more difficult


## pure recursion

```js
function collectOddValues(arr) {
  let newArr = [];

  if (arr.length === 0) {
    return newArr;
  }

  if (arr[0] % 2 !== 0) {
    newArr.push(arr[0]);
  }

  newArr = newArr.concat(collectOddValues(arr.slice(1)));
  return newArr;
}
```

pure recursion tips:
- for arrays, use methods like **slice/spread operator/concat** that makes copies of arrays so you don't mutate them
- remembre that strings are immutable so you'll need to use methods lie **slice/substr/substring** to make copies of strings
- to make copies of objects, use **Object.assign/spread operator**




































