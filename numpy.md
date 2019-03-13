## Slice Notation

*2019-02-21*

```python
a[start:end] # items start through end-1
a[start:]    # items start through the rest of the array
a[:end]      # items from the beginning through end-1
a[:]         # a copy of the whole array
a[start:end:step] # start through not past end, by step
```

Note that **end-1** is the last element of the array.

[SOF Link](https://stackoverflow.com/questions/509211/understanding-slice-notation)

*2019-02-22*

[Useful basic Python notes compilation](http://cs231n.github.io/python-numpy-tutorial/)

A slice of an array is a **view** into the same data, so modifying it will modify the original array.
```python
a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])
b = a[:2, 1:3]
print(a[0, 1])   # Prints "2"
b[0, 0] = 77     # b[0, 0] is the same piece of data as a[0, 1]
print(a[0, 1])   # Prints "77"
```

A mixture of **integer slicing** and **index slicing** is supported, but tricky.
```python
a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])

# Two ways of accessing the data in the middle row of the array.
# Mixing integer indexing with slices yields an array of lower rank,
# while using only slices yields an array of the same rank as the
# original array:
row_r1 = a[1, :]    # Rank 1 view of the second row of a
row_r2 = a[1:2, :]  # Rank 2 view of the second row of a
print(row_r1, row_r1.shape)  # Prints "[5 6 7 8] (4,)"
print(row_r2, row_r2.shape)  # Prints "[[5 6 7 8]] (1, 4)"

# We can make the same distinction when accessing columns of an array:
col_r1 = a[:, 1]
col_r2 = a[:, 1:2]
print(col_r1, col_r1.shape)  # Prints "[ 2  6 10] (3,)"
print(col_r2, col_r2.shape)  # Prints "[[ 2]
                             #          [ 6]
                             #          [10]] (3, 1)"

# This will not work:
b = a[[1,2], [1,2,3]]
# This will work instead:
b = a[[[1],[2]], [[1,2,3]]]
```

[SOF Link](https://stackoverflow.com/questions/21349133/numpy-array-integer-indexing-in-more-than-one-dimension)

***

## max / amax / maximum / argmax

*2019-02-21*

**np.max**: returns the **single** max element from a (maybe multi-dimensional) array  
**np.amax**: returns a array, with the max element from a array per a certain **axis**  
**np.maximum**: returns the **element-wise** max from **two** arrays

Examples:
```python
>>> a = np.array([[0, 1, 6],
                  [2, 4, 1]])
>>> np.max(a)
6

>>> np.max(a, axis=0) # max of each column
array([2, 4, 6])

>>> b = np.array([3, 6, 1])
>>> c = np.array([4, 2, 9])
>>> np.maximum(b, c)
array([4, 6, 9])

>>> d = np.argmax(a)
2
```

[SOF Link](https://stackoverflow.com/questions/33569668/numpy-max-vs-amax-vs-maximum)

In case the array is empty, we can check the emptiness by:

```python
if array.size:
    ...
```

***

## numba

*2019-02-22*

Numba is a just-in-time compiler for Python that works best on code that uses NumPy arrays and functions, and loops.  

Numba works well on code that looks like this:  

```python
from numba import jit
import numpy as np

x = np.arange(100).reshape(10, 10)

@jit(nopython=True) # Set "nopython" mode for best performance, equivalent to @njit
def go_fast(a): # Function is compiled to machine code when called the first time
    trace = 0
    for i in range(a.shape[0]):   # Numba likes loops
        trace += np.tanh(a[i, i]) # Numba likes NumPy functions
    return a + trace              # Numba likes NumPy broadcasting

print(go_fast(x))
```

[Official numba guide](https://numba.pydata.org/numba-doc/latest/user/5minguide.html)  
[SOF: why numba is faster?](https://stackoverflow.com/questions/25950943/why-is-numba-faster-than-numpy-here)

***

## Element-wise addition of lists

*2019-03-06*

Method 1: use **map** with **operator.add**:

```python
from operator import add
list(map(add, list1, list2))
```

Method 2: use **zip** with a list comprehension:

```python
[sum(x) for x in zip(list1, list2)]
```

[SOF: Element-wise addition of lists](https://stackoverflow.com/questions/18713321/element-wise-addition-of-2-lists)

***

## List pop()

*2019-03-06*

The pop() method removes the item at the given index from the list.

If the index passed to the pop() method is not in range, it throws IndexError: pop index out of range exception.

The parameter passed to the pop() method is optional. If no parameter is passed, the default index **-1** is passed as an argument which returns the **last** item.

This method is very handy, for instance if we are to remove the smallest item from the list:

```python
list.sort(reverse=True).pop()
```

***

## numpy is slow with for loops

*2019-03-07*

```python
import numpy as np

example = np.ones([500,500,500], dtype=np.uint8)

def slow():
     img = example.copy()
     height, width, depth = img.shape
     for i in range(0, height):             #looping at python speed...
         for j in range(0, (width//4)):     #...
             for k in range(0,depth):       #...
                 img[i,j,k] = 0
     return img


def fast():
     img = example.copy()
     height, width, depth = img.shape
     img[0:height, 0:width//4, 0:depth] = 0 # DO THIS INSTEAD
     return img 

np.alltrue(slow() == fast())
Out[22]: True

%timeit slow()
1 loops, best of 3: 6.13 s per loop

%timeit fast()
10 loops, best of 3: 40 ms per loop
```

[SOF: slow for loops](https://stackoverflow.com/questions/26445153/iterations-through-pixels-in-an-image-are-terribly-slow-with-python-opencv)

Also, **deepcopy()** is extremely slow. There's some analysis on SOF.

[SOF: deepcopy() vs copy()](https://stackoverflow.com/questions/24756712/deepcopy-is-extremely-slow/29385667#29385667)

***

## create a matrix of random numbers

*2019-03-12*

Use **np.random.rand()** to achieve this:

```python
>>> import numpy as np
>>> np.random.rand(2,3)
array([[ 0.22568268,  0.0053246 ,  0.41282024],
       [ 0.68824936,  0.68086462,  0.6854153 ]])
```

***

