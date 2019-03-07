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

***
