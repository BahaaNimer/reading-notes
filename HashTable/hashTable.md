# Hash Tables

## What is a Hashtable?

- Hash - A hash is the result of some algorithm taking an incoming string and converting it into a value that could be used for either security or some other purpose. In the case of a hashtable, it is used to determine the index of the array.
- Buckets - A bucket is what is contained in each index of the array of the hashtable. Each index is a bucket. An index could potentially contain multiple key/value pairs if a collision occurs.
- Collisions - A collision is what happens when more than one key gets hashed to the same location of the hashtable.

## Why do we use them?

1. Hold unique values
2. Dictionary
3. Library

## What Are they?

Hashtables are a data structure that utilize key value pairs. This means every `Node` or `Bucket` has both a key, and a value.

The basic idea of a hashtable is the ability to store the key into this data structure, and quickly retrieve the value. This is done through what we call a `hash`. A `hash` is the ability to encode the key that will eventually map to a specific location in the data structure that we can look at directly to retrieve the value.

Since we are able to `hash` our key and determine the exact location where our value is stored, we can do a lookup in an O(1) time complexity. This is ideal when quick lookups are required.

## Structure

### Hashing

Basically, a hash code turns a key into an integer. It’s very important that hash codes are deterministic: their output is determined only by their input. Hash codes should never have randomness to them. The same key should always produce the same hash code.

### Creating a Hash

A hashtable traditionally is created from an array. I always like the size 1024. this is important for index placement. After you have created your array of the appropriate size, do some sort of logic to turn that “key” into a numeric number value. Here is a simplistic hashing algorithm:

1. Add or multiply all the ASCII values together.
2. Multiply it by a prime number such as 599.
3. Use modulo to get the remainder of the result, when divided by the total size of the array.
4. Insert into the array at that index.

Example:

```js
Key = "Cat"
Value = "Josie"

67 + 97 + 116 = 280

280 * 599 = 69648

69648 % 1024 = 16

Key gets placed in index of 16.
```

### Collisions

A collision occurs when more than one key hashes to the same index in an array. As mentioned earlier, a “perfect hash” will never have any collisions. To put this into perspective, the worst possible hash is one that hashes every single key to the same exact index of an array. The more keys you have hashed to a specific index, the more key/value pair combos you can potentially have.

What would happen if two different keys resolved to be the same index of the array? This is called a collision. The hash map needs to be able to handle two keys resolving to the same index.

If two keys ever ultimately resolved to the same index, then two calls to `.Add(key, val)` with different keys would overwrite each other.

Collisions are solved by changing the initial state of the buckets. Instead of starting them all as `null` we can initialize a `LinkedList` in each one! Now if two keys resolve to the same index in the array then their key/value pairs can be stored as a node in a linked list. Each index in the array is called a “bucket” because it can store multiple key/value pairs.

Since different keys can lead to the same bucket it’s important to store the entire key/value pair in the bucket, not just the value. The key must be stored with the value! If only values were stored in buckets then it would be impossible to determine which value to return when a key led you to a bucket.

### Hash maps do this to store values

- accept a key
- calculate the hash of the key
- use modulus to convert the hash into an array index
- store the key with the value by appending both to the end of a linked list

### Hash maps do this to read value

- accept a key
- calculate the hash of the key
- use modulus to convert the hash into an array index
- use the array index to access the short LinkedList representing a bucket
- search through the bucket looking for a node with a key/value pair that matches the key you were given

### Bucket Sizes

Hash Maps can have any number of `buckets`. If a hash map has only a few `buckets` it will be densely full and have many collisions. If a hash map has more `buckets` it will be more sparsely populated, there will be less collisions, but there may be a lot of extra empty space.

It’s possible to compute the “`load factor`” of a hash table. The `load factor` tells us something about how full the hash table is. A hash table can start with only a few `buckets`, calculate it’s own `load factor`, recognize when it gets too full and automatically grow and add more `buckets` to itself to accommodate more data.

`Recognize`: calculating `load factor`s and choosing the optimal number of `buckets`, and determining the best hash functions is not within the scope of this class. This class intends to introduce you to what a hash table is, how it’s implemented, what hash codes are, how to handle collisions and how to reason generally about what it means for a hash table to be more empty or more full. This class does not intend to calculate theoretical optimal performance limits for how to best balance a Hash Table.

Here’s what the same information looks like in two different hash tables. The first hash table only has 7 `buckets`. The second has 100 `buckets`. Notice that even though the second hash table has 100 `buckets` there are still some collisions. Collisions are ok! We just don’t want every key to hash to the exact same index. That would be literally the worst!

## Internal Methods

### Add()

When adding a new key/value pair to a hashtable:

1. send the key to the `GetHash` method.
2. Once you determine the index of where it should be placed, go to that index
3. Check if something exists at that index already, if it doesn’t, add it with the key/value pair.
4. If something does exist, add the new key/value pair to the data structure within that bucket.

### Find()

The `Find` takes in a key, gets the Hash, and goes to the index location specified. Once at the index location is found in the array, it is then the responsibility of the algorithm the iterate through the bucket and see if the key exists and return the value.

### Contains()

The `Contains` method will accept a key, and return a bool on if that key exists inside the hashtable. The best way to do this is to have the contains call the `GetHash` and check the hashtable if the key exists in the table given the index returned.

### GetHash()

The `GetHash` will accept a key as a string, conduct the hash, and then return the index of the array where the key/value should be placed.

## Reference

[Hash Table](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-30/resources/Hashtables.html)
