# Custom 

## What is a Custom Iterator in Python?
A class designed to allow standard looping mechanisms (like `for` loops) to interact with a specific object, dispensing its contents one item at a time strictly on demand.

## Why use a Custom Iterator instead of a standard List?
- **Memory Efficiency:** Lists store all data in memory at once (Warehouse). Iterators generate data one piece at a time (Vending Machine), preventing crashes with massive datasets.
- **Infinite Sequences:** You can model infinite series (e.g., Even Numbers) which are impossible with lists.
- **Complex Logic:** It allows traversing non-linear structures (like trees) by defining specific rules for "what comes next."

## What two "dunder" methods constitute the Python Iterator Protocol?
1. `__iter__(self)`
2. `__next__(self)`

## What is the specific responsibility of the `__iter__` method in a custom iterator?
It acts as the setup/handshake. It must return the iterator object itself (`return self`) so the loop knows the object is ready to be iterated over.

## What is the specific responsibility of the `__next__` method?
It acts as the dispenser. It must:
1. Calculate/retrieve the next item based on current state.
2. Update the state (so the next call gets new data).
3. Return the item OR raise a signal to stop.

## How does a Custom Iterator remember its position (state) between calls?
It uses `self` to attach attributes to the instance (e.g., `self.current_index` or `self.counter`). Unlike a standard function which forgets local variables upon returning, the class instance persists data in memory.

## How does an iterator signal to a loop that there is no more data?
By raising the `StopIteration` exception.

## Why does an iterator raise `StopIteration` instead of returning a specific value (like `None` or `-1`) to signal the end?
Because `None`, `-1`, or `False` could be valid data items inside the iterator. An exception is a distinct "hard stop" signal that cannot be confused with the data content.

## What happens "under the hood" when a Python `for` loop encounters a `StopIteration` exception?
The loop catches the exception and interprets it as a signal to exit gracefully. It does **not** print an error message to the console; it simply stops looping.

## Complete the code for this simple counter iterator:
```python
class Counter:
    def __init__(self, limit):
        self.limit = limit
        self.count = 0

    def __iter__(self):
        # FILL IN THIS LINE

    def __next__(self):
        if self.count < self.limit:
            self.count += 1
            return self.count
        else:
            # FILL IN THIS LINE
```
```python
    def __iter__(self):
        return self  # The Handshake

    def __next__(self):
        if self.count < self.limit:
            self.count += 1
            return self.count
        else:
            raise StopIteration  # The Red Light
```

## Explain the "Warehouse vs. Vending Machine" analogy regarding Lists and Iterators.
- **List (Warehouse):** Stores the entire inventory in physical space at once. Requires huge capacity.
- **Iterator (Vending Machine):** Holds logic, not just stock. It dispenses one item at a time when a specific button (`__next__`) is pressed.

## If you implement `__next__` but forget to implement `__iter__`, what happens when you try to loop over the object?
Python raises a `TypeError: 'object' is not iterable`. The loop looks for the handshake (`__iter__`) first and fails immediately if it's missing.

## What happens if you create an iterator that never raises `StopIteration`?
It becomes an infinite iterator. If placed in a `for` loop without a manual `break` condition, the loop will run forever (or until the program crashes).

## In terms of "State Management," what is the sequence of events inside `__next__`?
1. **Look** at the current state (e.g., `self.counter`).
2. **Save** that value to a temporary variable (if you need to return the *current* state before incrementing).
3. **Update** the state (increment `self.counter`) for the *next* call.
4. **Return** the saved value.

## Given the following code, why will the loop run 0 times?
```python
class BadIterator:
    def __iter__(self):
        return self
    def __next__(self):
        raise StopIteration
        return 1

for x in BadIterator():
    print(x)
```
Because `StopIteration` is raised immediately upon the first call to `__next__`. The loop sees the "Red Light" instantly and exits before processing any data.