

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

