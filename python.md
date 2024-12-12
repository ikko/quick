Here's a **Python Built-in Functions Cheatsheet**, which includes essential built-in functions and commonly used libraries such as `itertools`, as well as other core Python features.

---

### **Python Built-in Functions Cheatsheet**

#### **1. Basic Built-in Functions**

- **`print()`**: Outputs data to the console.
    ```python
    print("Hello, World!")
    ```

- **`len()`**: Returns the length (number of items) of an object.
    ```python
    len("Hello")  # 5
    ```

- **`type()`**: Returns the type of an object.
    ```python
    type(5)  # <class 'int'>
    ```

- **`range()`**: Generates a sequence of numbers (useful for loops).
    ```python
    range(5)  # Generates: 0, 1, 2, 3, 4
    ```

- **`abs()`**: Returns the absolute value of a number.
    ```python
    abs(-5)  # 5
    ```

- **`sum()`**: Returns the sum of an iterable (e.g., list).
    ```python
    sum([1, 2, 3])  # 6
    ```

- **`min()` and `max()`**: Return the smallest and largest item in an iterable, respectively.
    ```python
    min([1, 2, 3])  # 1
    max([1, 2, 3])  # 3
    ```

- **`sorted()`**: Returns a sorted list from an iterable.
    ```python
    sorted([3, 1, 2])  # [1, 2, 3]
    ```

- **`reversed()`**: Returns a reversed iterator.
    ```python
    list(reversed([1, 2, 3]))  # [3, 2, 1]
    ```

- **`all()`**: Returns `True` if all elements of an iterable are true.
    ```python
    all([True, True, False])  # False
    ```

- **`any()`**: Returns `True` if any element of an iterable is true.
    ```python
    any([True, False, False])  # True
    ```

- **`enumerate()`**: Returns an iterator that produces tuples containing the index and value from an iterable.
    ```python
    list(enumerate(["a", "b", "c"]))  # [(0, 'a'), (1, 'b'), (2, 'c')]
    ```

- **`zip()`**: Combines multiple iterables element-wise into tuples.
    ```python
    list(zip([1, 2], ["a", "b"]))  # [(1, 'a'), (2, 'b')]
    ```

- **`map()`**: Applies a function to all items in an iterable.
    ```python
    list(map(lambda x: x * 2, [1, 2, 3]))  # [2, 4, 6]
    ```

- **`filter()`**: Filters elements from an iterable based on a condition.
    ```python
    list(filter(lambda x: x > 2, [1, 2, 3]))  # [3]
    ```

- **`round()`**: Rounds a floating-point number to a specified number of decimal places.
    ```python
    round(3.14159, 2)  # 3.14
    ```

- **`re.compile()`**: Compiles a regular expression pattern into a regex object.
    ```python
    import re
    pattern = re.compile(r"\d+")
    ```

---

#### **2. `itertools` Module Functions**

- **`itertools.count(start=0, step=1)`**: Infinite iterator, returns evenly spaced values starting from the `start` value.
    ```python
    import itertools
    list(itertools.count(10, 2))  # [10, 12, 14, 16, 18, ...]
    ```

- **`itertools.cycle(iterable)`**: Cycles through the iterable indefinitely.
    ```python
    list(itertools.islice(itertools.cycle([1, 2, 3]), 6))  # [1, 2, 3, 1, 2, 3]
    ```

- **`itertools.repeat(item, times)`**: Repeats the item a specified number of times.
    ```python
    list(itertools.repeat("a", 3))  # ['a', 'a', 'a']
    ```

- **`itertools.chain(*iterables)`**: Chains multiple iterables together into one.
    ```python
    list(itertools.chain([1, 2], [3, 4], [5, 6]))  # [1, 2, 3, 4, 5, 6]
    ```

- **`itertools.combinations(iterable, r)`**: Returns all possible combinations of length `r` from an iterable.
    ```python
    list(itertools.combinations([1, 2, 3], 2))  # [(1, 2), (1, 3), (2, 3)]
    ```

- **`itertools.permutations(iterable, r)`**: Returns all possible permutations of length `r` from an iterable.
    ```python
    list(itertools.permutations([1, 2, 3], 2))  # [(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]
    ```

- **`itertools.product(*iterables)`**: Returns the Cartesian product of multiple iterables.
    ```python
    list(itertools.product([1, 2], ['a', 'b']))  # [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b')]
    ```

- **`itertools.islice(iterable, start, stop, step)`**: Returns a sliced iterator.
    ```python
    list(itertools.islice([1, 2, 3, 4, 5], 1, 4))  # [2, 3, 4]
    ```

---

#### **3. File I/O Built-in Functions**

- **`open()`**: Opens a file and returns a file object.
    ```python
    file = open('file.txt', 'r')
    ```

- **`read()`**: Reads the entire file content.
    ```python
    content = file.read()
    ```

- **`readline()`**: Reads the next line from the file.
    ```python
    line = file.readline()
    ```

- **`write()`**: Writes content to a file.
    ```python
    with open('file.txt', 'w') as file:
        file.write("Hello, World!")
    ```

- **`close()`**: Closes the file object.
    ```python
    file.close()
    ```

---

#### **4. Object and Type Functions**

- **`isinstance()`**: Checks if an object is an instance of a class or a subclass.
    ```python
    isinstance(5, int)  # True
    ```

- **`issubclass()`**: Checks if a class is a subclass of another class.
    ```python
    issubclass(bool, int)  # True
    ```

- **`id()`**: Returns the identity of an object.
    ```python
    id("hello")  # Unique identifier for the string object
    ```

- **`getattr()`**: Gets the value of an attribute of an object.
    ```python
    class MyClass:
        x = 10
    obj = MyClass()
    getattr(obj, 'x')  # 10
    ```

- **`setattr()`**: Sets the value of an attribute of an object.
    ```python
    setattr(obj, 'x', 20)
    ```

- **`delattr()`**: Deletes an attribute of an object.
    ```python
    delattr(obj, 'x')
    ```

---

#### **5. Lambda Functions and Higher-Order Functions**

- **`lambda`**: Defines an anonymous function.
    ```python
    add = lambda x, y: x + y
    add(2, 3)  # 5
    ```

- **`filter()`**: Filters elements based on a function.
    ```python
    filter(lambda x: x > 5, [1, 6, 3])  # [6]
    ```

- **`map()`**: Applies a function to all items in an iterable.
    ```python
    map(lambda x: x**2, [1, 2, 3])  # [1, 4, 9]
    ```

- **`reduce()`** (from `functools`): Applies a binary function cumulatively to items in an iterable.
    ```python
    from functools import reduce
    reduce(lambda x, y: x + y, [1, 2, 3])  # 6
    ```

---

#### **6. Exception Handling**

- **`try`, `except`**: Used to handle exceptions in code.
    ```python
    try:
        x = 1 / 0
    except ZeroDivisionError:
        print("Cannot divide by zero")
    ```

- **`else`**: Runs if no exception is raised.
    ```python
    try:
        x = 1 / 1
    except ZeroDivisionError:
        print("Error")
    else:
        print("Success")
    ```

- **`finally`**: Always runs, whether an exception occurred or not.
    ```python
    try:
        x = 1 / 1
    finally:
        print("This always runs")
    ```

---

### **Summary Table**

| **Function**       | **Description**                                          |
|--------------------|----------------------------------------------------------|
| `len()`            | Get length of an iterable or string.                     |
| `range()`          | Generate a sequence of numbers.                          |
| `sum()`            | Sum of all elements in an iterable.                      |
| `sorted()`         | Return a sorted version of an iterable.                  |
| `all()`            | Returns `True` if all elements are true.                 |
| `any()`            | Returns `True` if any element is true.                   |
| `enumerate()`      | Returns index-value pairs of an iterable.                |
| `zip()`            | Combine multiple iterables into tuples.                  |
| `itertools.count()`| Infinite iterator that counts from a start value.        |
| `itertools.cycle()`| Cycles through an iterable.                             |
| `open()`           | Opens a file for reading or writing.                     |
| `map()`            | Applies a function to an iterable.                       |
| `filter()`         | Filters elements based on a condition.                   |

---

This cheatsheet covers essential **Python built-in functions**, from common utilities to more advanced functions like those in **itertools**. It should serve as a useful reference for day-to-day Python programming.