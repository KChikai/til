# Chainer Tips 

chainer関連の内容を書く．

<br>

## 内積計算

```python
import numpy as np
from chainer import Variable
import chainer.functions as F

l = Variable(np.array([1,2,3], np.float32))
l2 = Variable(np.array([1,0,2], np.float32))
print(F.matmul(l, l2, transa=True).data)       # >>> [[ 7.]] 二次元配列（行列）の場合，三次元配列となる
```


## モデルの保存

Chainer (ver1.5 ~) からserializerを用いることによって，
CPUとGPU間のモデルを考慮せずに保存が可能となっている．
モデルの保存は以下の通り．

```python
from chainer import serializer

# save a model (hdf5 or npz)
serializer.save_hdf5(filename, model)
serializer.save_npz(filename, model)

# load (hdf5 or npz)
serializer.save_hdf5(filename, model)
serializer.save_npz(filename, model)

```

optimizerも同様の記述で保存が可能．