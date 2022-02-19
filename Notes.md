---
marp: true
footer: #PyTexas 2022 - Choosing the Right Data Type
paginate: true
style: |
    table {
        margin-top: 1em;
        align: center;
    }
    
---

# Choosing the Right Data Type

**Josh Schneider**
[github/dijital20](https://github.com/dijital20)

<div style="margin-top: 4em;">

*Good programmers worry about data structures and their relationships.* 
[-- Linus Torvalds](https://www.defprogramming.com/q/f75f5dee011f/)

</div>

<!-- 
_class: invert 
_footer: ""
_paginate: false
-->

---

## Where did this come from?

* *"When should I use a list vs a tuple?"*
* *"Why does everything have to be a list/dict?"*
* The data structures we use send signals to users of our code on how the data matters and should be used.
* We're not going to cover "Elemental" data types (`int`, `str`, `float`, `bool`, `None`).

<!-- 
    Speaker Notes:
    I've been training some junior developers for a few years, and before that, I taught the most junior developer... 
    myself. During this time, I've seen the question, sometimes from my students and other times from my self; "do I use
    a list or a tuple here?", "Why does every collection have to be a list? Why does everything have to be nested 
    dictionaries?"

    Before my time as a senior developer, I was a technical support agent. In my time of helping customers overcome 
    problems with computers, calculators, and various applications; I learned to value the user experience. We usually
    think of user experience in terms of Graphical User Interfaces, or workflows; but we don't always think of them in 
    code. Each language has its own culture and expectations, and the choice of tools and how you use them send signals
    to the users of your code on how they should interpret, use, and extend the data they get.

    We're not going to focus on the elemental data types, like int, float, str, bool, and None. I call those elemental data
    types because you can't really break them down into anything simpler (without transmuting them into each other) and
    the data types we are going to talk about are really just ways of arranging values in those types.
 -->

<!-- ---

## Terminology

* **Immutable** types change by **moving the reference**, not changing the data.
* **Mutable** types change by **changing the data**, not moving the reference.
* **Ordered** types focus on **position** over value.
* **Unordered** types focus on **value** over position. -->

<!-- 
    Speaker Notes:
    This is a key thing to understand.

    All value assignment and passing in Python is by reference. When you assign a value to a name, you are binding a 
    reference to that value in memory to the name, so that when you call that name, you mean that location in memory.

    Immutable data types (all of our elemental data types are immutable) cannot be changed in their location in memory once
    assigned. This means that, say, adding to a string, requires you to construct a new string and then move the name to 
    point to a different reference in memory. This is how all immutable types work.

    Mutable data types can be changed in their location in memory. So when you pass a mutable data type instance to a 
    function, the function is receiving the reference to the same source of data. If either the function or the original
    context change the data, it will be present in both places.

    This is important to understand going forward.

    For ordered collections, focus is in the position of data within the set. For unordered collections, focus is on the 
    value of the data itself within the set.
 -->

<!-- JRS: Commenting out this slide for now. I think I can explain this on the table of the next slide. -->

---

## `list`, `set`, `tuple` - 3 very different bags

|Name       |Mutable    |Unique     |Ordered    |Useful methods                                 |
|---        |:-:        |:-:        |:-:        |---                                            |
|`list`     |&#10004;   |&#10060;   |&#10004;   |`push`, `pop`, `insert`, `append`, `extend`    |
|`set`      |&#10004;   |&#10004;   |&#10060;   |`union`, `intersection`, `difference`, `add`   |
|`tuple`    |&#10060;   |&#10060;   |&#10004;   |*tumbleweeds...*                               |

<!-- 
    Speaker Notes:
 -->

---

## `list`, `set`, `tuple` (cont.)

Use a `set` if all elements will be hashable, you need for all elements to be unique, and order doesn't matter.

Use a `tuple` when you are "packaging" values (passing around more than one value) or in places where you don't want the collection to be modified after created.

Use a `list` when order matters and you don't know how many items you have.

<!-- 
    Speaker Notes:
 -->

---

## `deque` - Popping and Locking and Pushing

Use a `deque` in place of a `list`:

- When you want to limit the total number of elements (`maxlen` is wonderful).
- When you want to use it as a stack, pushing items in one and and popping out of the other (they are marginally faster).

<!-- 
    Speaker Notes:
 -->

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

<!-- 
    Speaker Notes:
 -->

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

<!-- 
    Speaker Notes:
 -->

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

<!-- 
    Speaker Notes:
 -->

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

<!-- 
    Speaker Notes:
 -->

---

## Thanks for coming, and good luck!

[Clone these slides](https://github.com/dijital20/pytexas2022-data-types) I made with [Marp](https://marpit.marp.app/)

Questions, comments, remarks, jokes, limericks and dad jokes
[GitHub: @Dijital20](https://github.com/dijital20)

<!-- _class: invert -->
