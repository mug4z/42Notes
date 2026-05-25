
## List

```python
mylist = ["apple", "banana", "cherry"]
```
https://www.w3schools.com/python/python_lists.asp
## Sequence of byte
```python
bytes = b'LOL'
```

## Python slices

```python
a = ("a", "b", "c", "d", "e", "f", "g", "h")  
x = slice(2)
print(a[x]) # "a","b"
```

also 
```python
a = ("a", "b", "c", "d", "e", "f", "g", "h") 
print(a[0:2]) # "a","b"
```

## hmac

hmac hash as bytes array
```python
    hashed1 = hmac.new(testSecret,testCount, sha1)
    hashed1.digest()
```

## Import
**Python module** is a file that has a `.py` extension
**Python package** is any folder that has modules inside it.
an `__init__.py` make sure that the direcory is viewed as a packages.

https://realpython.com/absolute-vs-relative-python-imports/

#python #QuickNotes 