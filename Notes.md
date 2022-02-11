---
marp: true
footer: #PyTexas 2022
paginate: true
---

# Choosing the Right Data Type

**Josh Schneider**
[github/dijital20](https://github.com/dijital20)

<!-- _class: invert -->

---

## What we're not covering

"Elemental" data types (`int`, `str`, `float`, `bool`)

---

## Basic Collections - `list`, `set`, `tuple`

|Name       |Mutable    |Unique |Ordered|
|---        |---        |---    |---    |
|`list`     |Y          |N      |Y      |
|`set`      |Y          |Y      |N      |
|`tuple`    |N          |N      |Y      |

---

## Basic Collections (cont.)

Use a `set` if all elements will be hashable, you need for all elements to be unique, and order doesn't matter.

Use a `tuple` when you are "packaging" values (passing around more than one value) or in places where you don't want the collection to be editable once created.

Use a `list` when order matters and you don't know how many items you have.

---

## `deque` - Popping and Pushing

Use a `deque` in place of a `list`:

* When you want to limit the total number of elements (`maxlen` is wonderful).
* When you want to use it as a stack, pushing items in one and and popping out of the other (they are marginally faster).

---

## `namedtuple` - Name your data

Consider using a `namedtuple`  anywhere you'd use a `tuple` for packaging values to put names on the data.

```python
from collections import namedtuple

# Traditional Tuple - What do these numbers mean?
>> (27, 5, 32)
(27, 5, 32)

# Named Tuple - much easier to read
>> TaskTotals = namedtuple('TaskTotals', 'todo,done,total')
>> totals = TaskTotals(27,5,32)
>> totals
TaskTotals(todo=27, done=5, total=32)
>> totals.todo, totals[0]
27, 27
```

---

## Mapping - `dict`

A mapping relates one piece of data to another.

`dict` requires all keys to be unique (like a `set`), but the values can be anything. They are good to use when you want to relate one piece of unique information to another piece of information.

`dict` objects have their own methods/properties, but often don't have specialized methods/properties to their data.

---

## Classes and `dataclass`



---
