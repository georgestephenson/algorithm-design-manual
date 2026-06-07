# Kangaroo

With this one I wrote

$$
v1 \times n + x1 = v2 \times n + x2 \\
n (v1 - v2) = x2 - x1 \\
n = \frac{x2 - x1}{v1 - v2}
$$

So if $n$ is a positive integer, that's the number of kangaroo steps.

But we need to check if $v2 = v1$ to avoid dividing by zero.

``` python
def kangaroo(x1, v1, x2, v2):
    if v1 == v2:
        return "YES" if x1 == x2 else "NO"
    
    n = (x2 - x1) / (v1 - v2)
    return "YES" if n > 0 and n == int(n) else "NO"
```