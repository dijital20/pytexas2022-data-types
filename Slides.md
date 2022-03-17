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
* *"Why does everything have to be a list of dicts???"*
* The properties of the data structures we choose imply how the data should be interpreted, processed, and extended.
* We're not going to cover "Atomic" data types (`int`, `str`, `float`, `bool`, `None`).

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

 ---

## My Guiding Design Principle

1. Make it **obvious**.
2. If you can't make it obvious, make it **familiar**.
3. If you can't make it familiar, make it **well-documented**.

<!-- 
    Speaker Notes:

    The best user experiences are with things that are obvious. No one has to tell you how to use it, you just know.

    In the absence of obvious, familiar is next best. Borrowing understanding from something else makes it easier to 
    gain a cognitive foothold.

    In the absence of familiar, documentation is your last option. Documentation is useful but daunting, so if you can 
    make it familiar or obvious, you are far better off.
 -->

<!-- ---

## Terminology

* **Immutable** types change by **moving the reference**, not changing the data (they are close-ended).
* **Mutable** types change by **changing the data**, not moving the reference (they are open-ended).
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

|Name       |Mutable    |Ordered    |Useful methods                                 |
|:-:        |:-:        |:-:        |:-:                                            |
|`list`     |&#10004;   |&#10004;   |`push`, `pop`, `insert`, `append`, `extend`    |
|`set`      |&#10004;   |&#10060;   |`union`, `intersection`, `difference`, `add`   |
|`tuple`    |&#10060;   |&#10004;   |*tumbleweeds...*                               |

<!-- 
    Speaker Notes:
    We usually talk about lists, sets, and tuples collectively (see what I did there?); but they are very different.

    Lists and sets are your standard mutable collections. They are good at holding an indeterminate amount of items, 
    when you need to access the items from more than one place. Tuples, on the other hand, are locked when defined 
    (something fun happens when you put a mutable type inside an immutable type... remember that Python is 
    "by reference") and aren't extendable... which makes them good for packaging, but bad for being a drop zone for new 
    members.

    Note the inverse relationship between requiring unique data values and ordered. 
    - Sets are containers where value (uniqueness) matters for locating a value, not position. Because of this, all of 
      your elements have to be hashable (immutable).
    - Lists are containers where position matters for locating a value, more than the value itself. You can put any kind 
      of data into a list, you can mix and match... the value matters less than its position within the list.
    - Tuples are like lists, except that they can't be changed or extended without destroying the old one and making the 
      new one.
 -->

---

## `list`, `set`, `tuple` (cont.)

Use a `set` if all elements will be hashable (immutable), you need for all elements to be unique, and order doesn't matter.

Use a `tuple` when you are "packaging" values (passing around more than one value) or in places where you don't want the collection to be modified after created.

Use a `list` when order matters and you don't know how many items you have.

<!-- 
    Speaker Notes:
    (I think the slide content speaks for itself here.)
 -->

---

## `deque` - Popping and Locking and Pushing

Use a `deque` in place of a `list`:

- When you want to limit the total number of elements (`maxlen` is wonderful).
- When you want to use it as a stack, linearly processing data.

<!-- 
    Speaker Notes:
    A deque is another mutable data structure that is optimized for getting things from either end but not so much in the middle. 
 -->

---

## `namedtuple` - Name your data

Consider using a `namedtuple` anywhere you'd use a `tuple` for packaging values, so that you can put names on the data inside.

```python
>>> ('Saurian Brandy', 5, 32)
('Saurian Brandy', 5, 32)  # What are you?
```

```python
>>> from collections import namedtuple
>>> TaskTotals = namedtuple('InventoryItem', 'item,have,need')
>>> totals = InventoryItem('Saurian Brandy', 5, 32)
>>> totals
InventoryItem(item='Saurian Brandy', have=5, need=32)  # Much more clear
>>> totals.todo, totals[1]
5, 5
```

<!-- 
    Speaker Notes:
    Since tuples can store any kind of data inside just like list, a problem arises in understanding what each element 
    signifies. This can make it harder for your users, or force them to rely on docstrings (please, please always do 
    these, and do them well) and documentation.

    Namedtuples are awesome in that they give you all of the same functionality as a tuple, but with the addition names, 
    which are printed when the value is printed, and you can use to access the data rather than index.

    Namedtuples cannot easily contain instance methods and properties... a class is better for those, but if you don't 
    need them, then a namedtuple is a lightweight, understandable alternative to a tuple.
 -->

---

## Mapping - `dict`

Use a `dict` when...
- You need to relate some unique value to some other value.
- Where the number/type of the unique values are dynamic.

```python
>>> enterprise_role_map = {
    'Picard': 'Captain',
    'LaForge': 'Engineer',
    'Kirk': 'Captain',
    'McCoy': 'Medical',
}
>>> enterprise_role_map['Picard']
'Captain'
>>> 'Worf' in enterprise_role_map
False
```

<!-- 
    Speaker Notes:
    Dictionaries are awesome and powerful. They are flexible mapping that allow you to associate a piece of immutable 
    data with some other piece of data (which can be mutable or immutable). The value of the key is important because it
    is expected to be unique and significant for location. The associated value, on the other hand, can be anything.

    Dictionaries are so useful that they are used all over the Python landscape. Instances of objects created from 
    classes contain a dictionary inside to track the instance state, namespaces like globals(), locals(), a loaded 
    module, etc all expose dictionaries that you can use to access and iterate values.

    Unfortunately, in my opinion, dictionaries get a little overused, and can be daunting when they are nested to 
    multiple layers.

    I prefer to use dictionaries in places where the structure (the collection of keys) is more fluid. For places where 
    a dictionary should contain specific keys, a namedtuple, class, or dataclass-decorated class would be far more 
    useful for ensuring that deterministic state.
 -->

---

## `defaultdict` - Ensuring default data/type

Use a `defaultdict` in place of a dict if your values are the same data type, to ensure a default value if a key isn't defined. This can save you a few lines of code.

```python
>>> non_dd = dict()
>>> non_dd['foo'].append('bar')
KeyError: 'foo' not defined.
```

```python
>>> from collections import defaultdict
>>> dd = defaultdict(default_factory=list)
>>> dd['foo'].append('bar')
>>> dd['foo']
['bar']
```

---

## Classes

Use a `class` over a `dict` when you want a rigid, deterministic structure for holding data (fields) and/or actions (methods) on that data.

```python
>>> class WarpDrive(object):
...     def __init__(self):
...         self.factor = 0
... 
...     def set_speed(factor: int) -> 'WarpDrive':
...         print(f'Changing warp factor from {self.factor} to {factor}')
...         self.factor = factor
...         return self
... 
...     def engage(self) -> None:
...         print('Oh no, not installed until Tuesday')
...
>>> WarpDrive().set_factor(6).engage()
Changing warp factor from 0 to 6
Oh no, not installed until Tuesday
```

<!-- 
    Speaker Notes:
    Classes are the alternative to a straight dictionary anytime you want to ensure that instances have a deterministic 
    set of fields. You can control behavior through your implementation, and ensure the fields you expect are there.
    You can use `vars()` to get the `dict` flavor of the instance, returning any fields defined (but not properties or 
    methods).

    While the other types we've talked about so far all hold values, a class can also define actions via its methods
    and properties. This helps define objects that not only HOLD data, but can ACT on that data.

    I prefer to go to classes anytime where the properties of the object are deterministic (I know ahead of time that,
    say, all WarpDrive objects will have a warp factor) that I want to ensure are there for me to interact with.
 -->

---

## `dataclass` - A more refined class for representing data

Use a `dataclass` anywhere you would use a class, but don't want to write the boilerplate around a class (`__str__`, `__init__`, `__eq__`, etc).

```python
>>> from dataclasses import dataclass
>>> @dataclass
... class CrewPerson(object):
...     name: str
...     role: str
...     service_length: int
...
>>> p = CrewPerson('Picard', 'Captain', 35)
>>> p
CrewPerson(name='Picard', role='Captain', service_length=35)
>>> p.name
'Picard'
```

<!-- 
    Speaker Notes:
    Dataclasses were added in Python 3, and are a decorator around a normal class. The class decorator uses static 
    fields and type hints for those fields to fill in the boilerplate magic method around a new class. This frees you
    from having to define things like `__str__`, `__repr__`, etc.

    Even though the dataclass decorator uses the annotations of the class fields to create the instance fields in the 
    object, it does not enforce those types at runtime (meaning a field defined as `foo: int` can have a `str` value).
    The decorator itself has some useful keyword arguments (such as being able to declare the instance objects as 
    `frozen`, which will make then functionally immutable), as does the `field` function provided for customizing field
    rules.

    If you have a number of fields in a class, and want to save yourself some work around the magic methods, dataclass
    is a type of borrowed magic that's there for the taking!
 -->

---

## Thanks for coming, and good luck!

[Clone these slides](https://github.com/dijital20/pytexas2022-data-types) I made with [Marp](https://marpit.marp.app/)

Questions, comments, remarks, jokes, limericks and dad jokes
[GitHub: @Dijital20](https://github.com/dijital20)

<!-- _class: invert -->
