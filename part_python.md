1. log module

```python
import time
import argparse

def logger(func):
    def wrapper(*args, **kw):
        t1 = time.time()
        print('[INFO] execute {}function'.format(func.__name__))
        result = func(*args, **kw)
        t2 = time.time()
        cost_time = t2 - t1
        print('[INFO] finished {} function, consuming: {} sec'.format(func.__name__,cost_time))
        return result
    return wrapper
```
