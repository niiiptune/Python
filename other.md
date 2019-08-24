## Print

*2019-03-07*

### Method 1: string modulo operator **%**

```python
print("Art: %5d, Price: %8.2f" % (453, 59.058))
```

Common conversion formats:

| **Conversion** | **Meaning** |
| --- | --- |
| d | Signed integer decimal. |
| f | Floating point decimal format. |
| s | String (converts any python object using str()). |

### Method 2: the string method **format** (the Pythonic way)

```python
print("Art: {0:5d}, Price: {1:8.2f}".format(453, 59.058))
# use keyword parameters
print("Art: {a:5d}, Price: {b:8.2f}".format(a=453, b=59.058))
```

[More details](https://www.python-course.eu/python3_formatted_output.php)

***

## raise / except

*2019-03-12*

```python
raise ValueError('A very specific bad thing happened')

try:
    some_code_that_may_raise_value_error()
except ValueError:
    print("Description of the error")
```

To handle an exception of out-of-range index:

```python
try:
    newlist.append(dlist[1])
except (IndexError, ValueError):
    pass
continue
```

[SOF: manually raise an exception](https://stackoverflow.com/questions/2052390/manually-raising-throwing-an-exception-in-python/24065533)

[SOF: out-of-range index exception](https://stackoverflow.com/questions/11902458/i-want-to-exception-handle-list-index-out-of-range)

***

## capitalize vs upper

*2019-08-24*

**s.capitalize()**: Cap first letter of the string only
**s.upper()**: Cap the entire string
