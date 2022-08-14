# Time & Datetime

- unix timestamp to datetime:
  - `datetime_obj = datetime.fromtimestamp(unix_ts)`
- datetime to unix timestamp:
  - `unix_ts = datetime_obj.timestamp()`
- Format a datetime object:
  - `datetime_obj.strftime("%Y-%m-%d-%H-%M-%S")`

## Timing Functions

- `timeit.timeit(code_str, number=n)` is the core timing functionality that will give you average time for code to complete
- example below gets the time for a neural network inference

``` python
import torch
from learning_warmstarts.neural_nets.models import FFNet
import timeit

n = 10000

model = FFNet((13,1024,2048,240), torch.nn.functional.relu)
model.eval()

model.load_state_dict(torch.load('SOA.pt'))

with torch.no_grad():
   dummy_input = torch.randn((13),dtype=torch.float)
   total_time = timeit.timeit('model(dummy_input)',number=n, globals=globals())
   print(f'{total_time / n}')
```

