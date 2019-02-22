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

***

## max / amax / maximum

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
```

[SOF Link](https://stackoverflow.com/questions/33569668/numpy-max-vs-amax-vs-maximum)
