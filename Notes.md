# Choosing the Right Data Type

* Focusing on "constructed" types, not "primitive" types.
* Types
  * tuple
    * Pros
      * Fixed length
      * Memory efficient
      * Immutable
    * Cons
      * Immutable
      * Fixed length
    * Use when
      * You need to package more than on value together, where the number of values are either fixed, or variable but immutability matters.
  * list
    * Pros
      * Variable length
      * Mutable
      * Can accept any type
    * Cons
      * Can accept any type
      * Mutable
    * Use when
      * You need a variable length collection of values that is flexible, and are willing to safeguard mutation yourself.
  * set
    * Pros
      * Ensure values are unique
      * Access to set operations (union, intersection, etc)
      * Fast when searching for values inside it.
    * Cons
      * Restricted to hashable (read: immutable) data types inside
      * Values are unordered (or rather, order isn't guaranteed)
      * Mutable
    * Use when
      * You need a variable length collection of values that are immutable, and would like to ensure non-unique values are ignored, or would like to use set operations.
  * dict
    * Pros
      * While keys must be hashable (immutable), values can be any type.
      * Mutable
      * Variable length
      * Maps an immutable value to another value.
      * Fast when searching for keys inside it.
    * Cons
      * Mutable
      * 
    * Use when
  * Namedtuple
    * Pros
      * All the same as a tuple
      * Assign names to slots, allowing attribute access in addition to index access
    * Cons
      * Fixed number of fields/values.
      * Immutable
    * Use when
      * When you (A) want to name the values contained inside and (B) want the option to use index access as well.
  * DefaultDict
    * Pros
    * Cons
    * Use when
  * deque
    * Pros
    * Cons
    * Use when
  * dataclass
    * Pros
    * Cons
    * Use when
  * class
    * Pros
    * Cons
    * Use when



## Flowed notes

### Basic Collections - `list`, `set`, `tuple`

|Name|Mutable|Unique|Ordered|
|---|---|---|---|
|`list`|Y|N|Y|
|`set`|Y|Y|N|
|`tuple`|N|N|Y|

`list` is a good go-to collection, when order matters and you don't know how many items you have or position has little meaning.

`set` is good if you need for all elements to be unique (they all must be hashable) and order doesn't matter.

`tuple` is good for "packaging" values (passing around more than one value) or places where you don't want the collection to be editable once created.

### `deque` and `namedtuple`

`deque` is better than a list if you need to use it like a stack (add items and/or remove items from one end or the other, but don't need to search through the middle) as they are optimized for this.

`namedtuple` is good if you need the indexability and immutability of a tuple, but also need to put labels on the data. These are good to use in place of tuples if you are "packaging" values to return.

```python
from collections import namedtuple

# Traditional Tuple - What do these numbers mean?
>> (27, 5, 32)
(27, 5, 32)

# Named Tuple - much easier to read
>> TaskTotals = namedtuple('TaskTotals', 'todo,done,total')
>> TaskTotals(27,5,32)
TaskTotals(todo=27, done=5, total=32)
>> TaskTotals(27,5,32).todo
27
>> TaskTotals(27,5,32)[0]
27
```

### Mapping

