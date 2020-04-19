# hash tables

hash tables are used to store key-value pairs

nearly every programming language has them built in, but we're going to try and write our own so that we can understand what is happening behind the scenes.

to implement a hash table, we'll be using an array
- in order to look up values by key, we need a way to **convert keys into valid array indices**
- the function that performs this task is called a **hash function**

### what makes a good hash?
1. fast (ie constant time)
  - when we fetch/update/remove, we want it to be fast
2. we want it to distribute things uniformly so that outputs at specific indices don't cluster
3. deterministic
  - every time we pass in one input, we always get the same output

lets go through an example and build up from there
simple hash example for strings only:
```js
function hashString(key, arrayLen) {
  let total = 0;
  for (let char of key) {
    // map "a" to 1, "b" to 2, "c" to 3, etc
    let value = char.charCodeAt(0) - 96;
    total = (total + value) % arrayLen;
  }
  return total;
}
```
problem with this current hash
- only hashes strings
- not constant time - linear in key length
- could be a little more random

```js
function hashString(key, arrayLen) {
  let total = 0
  let WEIRD_PRIME = 31;
  for (let i = 0; i < Math.min(key.length, 100); i++) {
    let char = key[i];
    let value = char.charCodeAt(0) - 96;
    total = (total * WEIRD_PRIME + value) % arrayLen;
  }
  return total;
}
```

- hashes almost always take advantage of prime numbers
  - reduces collisions - we don't want data to be stored in the same bucket, we want to make sure that we're spreading data out so that they're faster to retrieve
  - it's also helpful if the array that you're putting values into has a prime length



























