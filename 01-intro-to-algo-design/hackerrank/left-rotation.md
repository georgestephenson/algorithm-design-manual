# Left Rotation

After learning this Python list slicing syntax, I could do this problem basically in one line

``` python
def rotateLeft(d, arr):
    arr[:-d], arr[-d:] = arr[d:], arr[:d]
    return arr
```

Although it's probably simpler to just write

``` python
def rotateLeft(d, arr):
    return arr[d:] + arr[:d]
```