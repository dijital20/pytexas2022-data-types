---
marp: true
footer: #PyTexas 2022 - Choosing the Right Data Type
paginate: true
---

# Choosing the Right Data Type

**Josh Schneider**
[github/dijital20](https://github.com/dijital20)

<!-- _class: invert -->
<!-- _footer: "" -->
<!-- _paginate: false -->

---

## Where did this come from?

* This question has come up from each junior developer I have trained, including myself!
  * *"When should I use a list vs a tuple?"*
  * *"Why does everything have to be a list/dict?"*
* We're not going to cover "Elemental" data types (`int`, `str`, `float`, `bool`, `None`).

---

## `list`, `set`, `tuple` - 3 very different bags


<center style="margin-top: 40px;">

|Name       |Mutable    |Unique |Ordered|Useful methods                                 |
|---        |:-:        |:-:    |:-:    |---                                            |
|`list`     |Y          |N      |Y      |`push`, `pop`, `insert`, `append`, `extend`    |
|`set`      |Y          |Y      |N      |`union`, `intersection`, `difference`, `add`   |
|`tuple`    |N          |N      |Y      |*tumbleweeds...*                               |

</center>

---

## `list`, `set`, `tuple` (cont.)

Use a `set` if all elements will be hashable, you need for all elements to be unique, and order doesn't matter.

Use a `tuple` when you are "packaging" values (passing around more than one value) or in places where you don't want the collection to be modified after created.

Use a `list` when order matters and you don't know how many items you have.

---

## `deque` - Popping and Locking and Pushing

Use a `deque` in place of a `list`:

- When you want to limit the total number of elements (`maxlen` is wonderful).
- When you want to use it as a stack, pushing items in one and and popping out of the other (they are marginally faster).

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

Use a `dict` when...
- You need to relate some immutable value to another value.
- Where the number and structure of the immutable values are dynamic.

```python
>> enterprise_role_map = {
    'Picard': 'Captain',
    'LaForge': 'Engineer',
    'Kirk': 'Captain',
    'McCoy': 'Medical',
}
>> enterprise_role_map['Picard']
'Captain'
>> 'Worf' in enterprise_role_map
False
```

---

## Classes

Use a `class` when you want a rigid deterministic structure for holding data (fields) and actions (methods) on that data.

```python
>> class WarpDrive(object):
..     def __init__(self):
..         self.factor = 0
.. 
..     def set_speed(factor: int) -> 'WarpDrive':
..         print(f'Changing warp factor from {self.factor} to {factor}')
..         self.factor = factor
..         return self
.. 
..     def engage(self) -> None:
..         print('Oh no, not installed until Tuesday')

>> WarpDrive().set_factor(6).engage()
Changing warp factor from 0 to 6
Oh no, not installed until Tuesday
```

---

## `dataclass` - A more refined class for representing data

Use a `dataclass` when you want a rigid, deterministic structure for holding data, don't want to write the boilerplate around a class, and don't need the indexability of a `namedtuple`.

```python
>> from dataclasses import dataclass
>> @dataclass
.. class CrewPerson(object):
..     name: str
..     role: str
..     service_length: int

>> p = CrewPerson('Picard', 'Captain', 35)
>> p
CrewPerson(name='Picard', role='Captain', service_length=35)
>> p.name
'Picard'
```
