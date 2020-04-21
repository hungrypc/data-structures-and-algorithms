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

### handling collisions
even with a large array and a great hash function, collisions are inevitable.

There are many ways to deal with collisins, but we'll focus on two:
1. separate chaining
2. linear probing

with *separate chaining*, at each index in our array we store values using a more sophisticated data structure (eg an array or linked list)
- this allows us to store multiple key-value pairs at the same index

with *linear probing*, when we find a collision, we search through the array to find the next empty slot
- unlike with separate chaining, this allows us to store a single key-value at each index


## writing our own HashTable

### starter code
```js
class HashTable {
  constructor(size=53) {
    this.keyMap = new Array(size);
  }

  _hash(key) {
    let total = 0;
    let WEIRD_PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      let char = key[i];
      let value = char.charCodeAt(0) - 96;
      total = (total * WEIRD_PRIME + value) % this.keyMap.length;
    }
    return total;
  }
}
```

### set/get
set:
- accepts a key and a value
- hashes the key
- stores the key-value pair in the hash table array via separate chaining

get:
- accepts a key
- hashes the key
- retrieves the key-value pair in the hash table
- if they key is not found, return undefined

```js
class HashTable {
  constructor(size=53) {
    this.keyMap = new Array(size);
  }

  _hash(key) {
    let total = 0;
    let WEIRD_PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      let char = key[i];
      let value = char.charCodeAt(0) - 96;
      total = (total * WEIRD_PRIME + value) % this.keyMap.length;
    }
    return total;
  }

  set(key, val) {
    const index = this._hash(key);
    if (!this.keyMap[index]) {
      this.keyMap[index] = [];
    }
    let keyExists = false;
    for (let i = 0; i < this.keyMap[index].length; i++) {
      if (key === this.keyMap[index][i][0]) {
        keyExists = true;
        this.keyMap[index][i][1] = val;
      }
    }
    if (!keyExists) this.keyMap[index].push([key, val]);
  }

  get(key) {
    const index = this._hash(key);
    if (this.keyMap[index]) {
      for (i = 0; i < this.keymap[index].length; i++) {
        if (this.keyMap[index][i][0] === key) {
          return this.keymap[index][i][1];
        }
      }
    }
    return undefined;
  }
}
```

### keys/values

keys (collect all the keys):
- loops through the hash table array and returns an array of keys in the table

values (collect all the values):
- loops through the hash table array and retruns an array of values in the table
```js
class HashTable {
  constructor(size=53) {
    this.keyMap = new Array(size);
  }

  _hash(key) {
    let total = 0;
    let WEIRD_PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      let char = key[i];
      let value = char.charCodeAt(0) - 96;
      total = (total * WEIRD_PRIME + value) % this.keyMap.length;
    }
    return total;
  }

  keys() {
    let keysArr = [];
    for (let i = 0; i < this.keymap.length; i++) {
      if (this.keyMap[i]) {
        for (let j = 0; j < this.keyMap[i].length; j++) {
          keysArr.push(this.keyMap[i][j][0]);
        }
      }
    }
    return keysArr;
  }

  values() {
    let valuesArr = [];
    for (let i = 0; i < this.keymap.length; i++) {
      if (this.keyMap[i]) {
        for (let j = 0; j < this.keyMap[i].length; j++) {
          valuesArr.push(this.keyMap[i][j][1]);
        }
      }
    }
    return valuesArr;
  }
}
```

### big O
average cases/best case in general:

method    | big O
----------|-------
insertion | O(1)
deletion  | O(1)
access    | O(1)

it is possible to write a hash function that is constant time, generally every programming language that has an implementation of a hash table has a constant time hash function
- different to a cryptographic hash function, which does need to take time -> hash function traverses every part of the data
