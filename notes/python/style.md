# Style Guide

- [PEP8 Style Guide](https://pep8.org/#introduction)
- [Google Style Guide](https://google.github.io/styleguide/pyguide.html) 

## Exceptions

- `ValueError`- indicate a programming mistake like a violated pre-condition
- Don't use catch-all `except`: statements 
- make code in try/except blocks as small as possible

## General

- Avoid global variables due to their potential to change module behavior during import
  - If needed, declare them at module level and make internal to module by prepending `_` to name
- Nested functions are fine, however they should have read-only access to variables defined in enclosing scope
  - Try to avoid in general and make helper functions private to module with `_` so they can still be tested
- Use `if foo is not None` instead of `if foo` b/c foo could be another value python evaluates as false (e.g `0`)
  - numpy arrays can raise exception in implicit boolean context -> test emptiness of `np.array` using `if not arry.size`
- Avoid using `@staticmethod` and instead write a module level function instead
- max line length of 80 chars
