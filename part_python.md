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

4. 进程池
```python
#coding: utf-8
import multiprocessing
import time

def func(msg):
    print "msg:", msg
    time.sleep(3)
    print "end"

if __name__ == "__main__":
    pool = multiprocessing.Pool(processes = 3)
    for i in xrange(4):
        msg = "hello %d" %(i)
        pool.apply_async(func, (msg, ))   #维持执行的进程总数为processes，当一个进程执行完毕后会添加新的进程进去

    print "Mark~ Mark~ Mark~~~~~~~~~~~~~~~~~~~~~~"
    pool.close()
    pool.join()   #调用join之前，先调用close函数，否则会出错。执行完close后不会有新的进程加入到pool,join函数等待所有子进程结束
    print "Sub-process(es) done."
```

