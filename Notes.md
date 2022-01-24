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