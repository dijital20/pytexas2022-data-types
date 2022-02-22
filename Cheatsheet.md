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
>> grocery_list = ['milk', 'eggs', 'spam']  # Make a list.
>> len(grocery_list)  # Find how many items are contained
3
>> grocery_list[1]  # Get an item by index
'eggs'
>> 'spam' in grocery_list  # Check for  an item
True
>> grocery_list.append('eggs')  # Append single items
>> grocery_list += ['cereal', 'cookies']  # Combine lists
>> grocery_list
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
>> grocery_set = {'milk', 'eggs', 'spam'}  # Create a set
>> len(grocery_set)  # Find how many items are contained
3
>> 'spam' in grocery_set  # Check for an item
True
>> grocery_set.add('eggs')  # Add an item
>> grocery_set.extend({'cereal', 'cookies'})  # Add multiple items
>> grocery_set
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

---

## `namedtuple`

### Essential Facts

- All of the power of a tuple, but allows you to add names to the values.
- Allows value access by index or by name.

### Use when

- You have a fixed number of values that you are grouping together, with each value having a meaning (name).

---

## `deque`

### Essential Facts

### Use when

---

## `dict`

### Essential Facts

### Use when

---

## `class`

### Essential Facts

### Use when

---

## `dataclass`

### Essential Facts

### Use when
