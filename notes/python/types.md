# Types 

- Code samples from [DeepMind's Robotics Repo](https://github.com/deepmind/dm_robotics/blob/main/py/vision/types.py)
  - Best practice to define all types for a package in a `types.py`
- Good type names reduces the need for building context in programmer's brain, makes it easier to read, and decreases the need for documentation
- Document design decisions, not what the code does (this can be inferred by reading it)

## Typing

- Can create complex type annotations:

``` python
from typing import Mapping, Optional, Sequence, Tuple

MaskPoints = Sequence[Sequence[Tuple[int, int]]]
Centers = Mapping[str, Optional[np.ndarray]]
Detections = Mapping[str, Optional[np.ndarray]]
```

## Dataclasses

- Setting frozen option makes the types immutable upon being instantiated

### Inheritance

- Can make the types more readable, even if no additional fields are added
- code serves as documentation

```python
import dataclasses

@dataclasses.dataclass(frozen=True)
class ValueRange:
  """A generic N-dimensional range of values in terms of lower and upper bounds.
  Attributes:
    lower: A ND array with the lower values of the range.
    upper: A ND array with the upper values of the range.
  """
  lower: np.ndarray
  upper: np.ndarray


@dataclasses.dataclass(frozen=True)
class ColorRange(ValueRange):
  """A range of colors in terms of lower and upper bounds.
  Typical usage example:
    # A YUV color range (cuboid)
    ColorRange(lower=np.array[0., 0.25, 0.25],
               upper=np.array[1., 0.75, 0.75])
  Attributes:
    lower: A 3D array with the lower values of the color range.
    upper: A 3D array with the upper values of the color range.
  """
```



### Optional Fields and Default Values

``` python
import dataclasses
from typing import Optional

@dataclasses.dataclass(frozen=True)
class Camera:
  """Camera parameters.
  Attributes:
    width: image width.
    height: image height.
    extrinsics: camera extrinsics.
    intrinsics: camera intrinsics.
  """
  width: int
  height: int
  extrinsics: Optional[Extrinsics] = None
  intrinsics: Optional[Intrinsics] = None
```

## Typing Module

- `list` instead of `List` is only 3.9+

- Type alias: `Vector = list[float]`

  - so those two are interchangeable
  - useful for simplifying complex type signatures

- NewType creates distinct types to catch logical errors 

  - declares a type to be a subtype of another

  ```python
  from typing import NewType
  
  UserId = NewType('UserId', int)
  some_id = UserId(524313)
  ```

- Frameworks expecting callback functions of specific signatures: `Callable[[Arg1Type, Arg2Type], ReturnType]`

  - `Callable[..., ReturnType]` if you don't care about call signature


## Enums
