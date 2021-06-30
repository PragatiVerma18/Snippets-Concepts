# Django Q & F

## Q objects
- With Q Objects, you can do more complex queries at once, support | (OR) and & (AND) operations.
- **Usage scenario:** There is only one filter query condition, while using Q can set multiple query conditions
- When using filter keyword query and Q query at the same time, be sure to put the Q object in front

### Resources
- [The power of django’s Q objects
](http://www.michelepasin.org/blog/2010/07/20/the-power-of-djangos-q-objects/)

---

## F() expressions
- F objects can avoid capturing the data in the database into the Python memory operation and then saving it back, but directly execute the SQL operation.
- When using Django's F() class, Python does not know what the value is stored in it. Instead, it generates the SQL for the operation and gives it to the database. After the operation is completed, the value in Python will not be updated. If a new value is required, it must be reloaded.
- As well as addition, Django supports subtraction, multiplication, division, and modulo arithmetic with F() objects, using Python constants, variables, and even other F() objects.
- **Performance advantages of F()**
  - Let the database to operate, not Python
  - Reduce the number of queries in some cases
  - Let the database (not Python) handle the race condition
  - The data will be manipulated according to the value in the database when SQL is executed, rather than the value of the Python memory previously captured. When there are multiple threads, the race condition can be processed by the database instead of being processed separately by Python.

### Resources
- [Django Q & F](https://gist.github.com/deadendif/36a6bf53af03006b1237)
---
