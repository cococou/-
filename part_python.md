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

2. 下载序列

```sh
esearch -db nucleotide -query "NC_007361.1"|efetch -format fasta > 102793.fa
```

3. 下载病毒序列

```sh
esearch -db nucleotide -query "txid12066[Organism]"|efilter -query "refseq"|efetch -format fasta > 12066.fa
```

