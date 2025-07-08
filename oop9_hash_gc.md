### Exercise – Point Class

Create a class named `Point` that represents a 2D point with coordinates `x` and `y`

#### Requirements:

1. In the constructor (`__init__`), receive the values `x` and `y`, and store them as private attributes
2. Write **getter** and **setter** methods for both attributes
3. Fully implement:

   * `__repr__`
   * `__str__`
   * `__eq__`
   * `__hash__` 
4. Create two points with the same values (e.g., `Point(3, 4)` and `Point(3, 4)`)
5. Store a value in a dictionary using the first object as a key (e.g., value should be the result of `sqrt(x^2 + y^2)`)
6. Add another value using the second object as a key (e.g., a string or a label of your choice)
7. Print the dictionary

#### Thinking Questions:

* How many items are actually stored in the dictionary and why
* What is a hash collision and can it happen here
* What is reference count in memory and how is it related to GC (garbage collection)


  כתובת הגשת התרגיל- pythonai250824+OOP9@gmail.com
