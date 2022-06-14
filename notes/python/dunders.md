# Dunder Methods


## `__call__()`

- Allows an instantiated class to be called like a function
- Similar to [Functor in C++](../../software_design/cpp/functors.md)
- Examples from [Stack Overflow](https://stackoverflow.com/questions/5824881/python-call-special-method-practical-example#comment6686265_5825015)

``` python
class Factorial:
    def __init__(self):
        self.cache = {}
    def __call__(self, n):
        if n not in self.cache:
            if n == 0:
                self.cache[n] = 1
            else:
                self.cache[n] = n * self.__call__(n-1)
        return self.cache[n]

fact = Factorial()
```

``` python
import hashlib

class Hasher:
    """
    A wrapper around the hashlib hash algorithms that allows an entire file to
    be hashed in a chunked manner.
    """
    def __init__(self, algorithm):
        self.algorithm = algorithm

    def __call__(self, file):
        hash = self.algorithm()
        with open(file, 'rb') as f:
            for chunk in iter(lambda: f.read(4096), ''):
                hash.update(chunk)
        return hash.hexdigest()

md5    = Hasher(hashlib.md5)
sha1   = Hasher(hashlib.sha1)
sha224 = Hasher(hashlib.sha224)
sha256 = Hasher(hashlib.sha256)
sha384 = Hasher(hashlib.sha384)
sha512 = Hasher(hashlib.sha512)

print(sha1('somefile.txt'))
```

