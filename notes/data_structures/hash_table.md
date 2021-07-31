##### Hashmaps:
- Built on top of an array using a special indexing system.
- A key-value storage with fast assignments and lookup.
- A table that represents a map from a set of keys to a set of values.
- Uses a hash function which turns a key into an index into the underlying array.
- A hash collision is when a hash function returns the same index for two different keys.
- Hash collision strategies:  
  - *Separate Chaining*- each array index points to a different data structure (e.g. array of linked lists)
  - *Open addressing*-a collision triggers a probing sequence to find where to store the value for a given key.

- Hash table: A key-value store that uses an array and a hashing function to save and retrieve values.
- Key: The identifier given to a value for later retrieval.
- Hash function: A function that takes some input and returns a number
  - Compression function: A function that transforms its inputs into some smaller range of possible outputs (e.g. Hash Function)
  - Key property is that it is not reversible 

Recipe for saving to a hash table:
- Take the key and plug it into the hash function, getting the hash code.
- Modulo that hash code by the length of the underlying array, getting an array index.
- Check if the array at that index is empty, if so, save the value (and the key) there.
- If the array is full at that index continue to the next possible position depending on your collision strategy.

Recipe for retrieving from a hash table:
- Take the key and plug it into the hash function, getting the hash code.
- Modulo that hash code by the length of the underlying array, getting an array index.
- Check if the array at that index has contents, if so, check the key saved there.
- If the key matches the one you're looking for, return the value.
- If the keys don't match, continue to the next position depending on your collision strategy.

