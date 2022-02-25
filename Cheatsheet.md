---
standalone: true
geometry: "margin=2cm"
---

# Data Types Cheatsheet

## `list`

### Essential facts

- Mutable
- Ordered
- Combinable
- Can use any type

### Use when
- You have an indeterminate amount of loosely related elements.
- Order matters.

### Example

```python
>>> grocery_list = ['milk', 'eggs', 'spam']  # Make a list.
>>> len(grocery_list)  # Find how many items are contained
3
>>> grocery_list[1]  # Get an item by index
'eggs'
>>> 'spam' in grocery_list  # Check for  an item
True
>>> grocery_list.append('eggs')  # Append single items
>>> grocery_list += ['cereal', 'cookies']  # Combine lists
>>> grocery_list
['milk', 'eggs', 'spam', 'eggs', 'cereal', 'cookies']
```

---

## `set`

### Essential facts
- Mutable
- Unordered
- Types stored in it MUST be hashable (immutable), and only unique values are stored.

### Use when
- When you have an indeterminate amount of loosely related elements.
- Uniqueness matters, but order does not

### Example

```python
>>> grocery_set = {'milk', 'eggs', 'spam'}  # Create a set
>>> len(grocery_set)  # Find how many items are contained
3
>>> 'spam' in grocery_set  # Check for an item
True
>>> grocery_set.add('eggs')  # Add an item
>>> grocery_set.extend({'cereal', 'cookies'})  # Add multiple items
>>> grocery_set
{'milk', 'eggs', 'spam', 'cereal', 'cookies'}
# Note that 'eggs' only appears once...
```

---

## `tuple`

### Essential Facts

- Immutable (once set, can't be changed)
- Ordered
- Can use any type

### Use when

- You either have a fixed number of values you are trying to group for convenience, or you hae an indeterminate amount of values that you don't want users to be able to change once defined.

```python
>>> this, that = 1, 2
>>> DEFAULT_VALUES = ('foo', 'bar', 'baz')
>>> # Using a tuple as default values so you aren't passing a mutable...
>>> def this_function_does_things(things_to_iterate = DEFAULT_VALUES):
...     results = []
...     # This could be a list comprehension, but being easy here...
...     for item in things_to_iterate:
...         if str(item).startswith('b'):
...             results.append(item)
...     return results
...
>>> this_and_that = (this, that)  # Packaging values to use.
>>> this_and_that[0]
1
```

---

## `namedtuple`

### Essential Facts

- All of the power of a tuple, but allows you to add names to the values.
- Allows value access by index or by name.

### Use when

- You have a fixed number of values that you are grouping together, with each value having a meaning (name).


```python
>>> from collections import namedtuple
>>> TaskTotals = namedtuple('InventoryItem', 'item,have,need')
>>> totals = InventoryItem('Saurian Brandy',5,32)
>>> totals
InventoryItem(item='Saurian Brandy', have=5, need=32)  # Much more clear
>>> totals.todo, totals[1]
5, 5
```

---

## `deque`

### Essential Facts

- Short for "double ended queue"
- Optimized for operations where you want to put or take from one end or the other.

### Use when

- You want to limit the number of items in the collection.
- You are going to be processing the contents of the collection linearly.

```python
>>> from collections import deque
>>> messages = deque(maxlen=5)
>>> for i in range(10):
...     messages.append(f'message {i}')
...     print(messages)
...
deque(['message 0'], maxlen=5)
deque(['message 0', 'message 1'], maxlen=5)
deque(['message 0', 'message 1', 'message 2'], maxlen=5)
deque(['message 0', 'message 1', 'message 2', 'message 3'], maxlen=5)
deque(['message 0', 'message 1', 'message 2', 'message 3', 'message 4'], maxlen=5)
deque(['message 1', 'message 2', 'message 3', 'message 4', 'message 5'], maxlen=5)
deque(['message 2', 'message 3', 'message 4', 'message 5', 'message 6'], maxlen=5)
deque(['message 3', 'message 4', 'message 5', 'message 6', 'message 7'], maxlen=5)
deque(['message 4', 'message 5', 'message 6', 'message 7', 'message 8'], maxlen=5)
deque(['message 5', 'message 6', 'message 7', 'message 8', 'message 9'], maxlen=5)
>>> messages.pop()
'message 9'
>>> messages.popleft()
'message 5'
>>> messages
deque(['message 6', 'message 7', 'message 8'], maxlen=5)
```

---

## `dict`

### Essential Facts

- Mapping of an immutable piece of data (the key) to a mutable or immutable piece of data (the value).
- Although order is deterministic in Python 3.7+, should not be relied on.
- Used all over the place in Python (instance objects, modules, globals, locals, etc)

### Use when

- You need to reference a unique piece of data to another piece of data.
- The number and contents of the keys are indeterminate.

```python
# TODO: Add an example here.
```

---

## `defaultdict`

### Essential Facts

- Initialize it with a `default_factory`, which can produce data if a key is undefined.
- Allows you to ensure that each key, if not defined, as a default value when accessed.

### Use when

- Your dictionary values are all a single type, and you want to ensure a default value is available for undefined keys.

```python
# TODO: Add an example here.
```

---

## `class`

### Essential Facts

### Use when

- The structure of data (fields and their value types) are deterministic (you know then ahead of time)
- You want to add "actions" (methods) in addition to the state data (fields).

```python
# TODO: Add an example here.
```

---

## `dataclass`

### Essential Facts

- Uses class fields and their associated type hints.
- Creates magic methods for you (`__init__`, `__str__`, `__eq__`, etc) so you don't have to.
- The `@dataclass` decorator has some great customizations.

### Use when

- You want to define a `class` that contains values, and you don't want to write a bunch of boilerplate magic methods.

```python
# TODO: Add an example here.
```
