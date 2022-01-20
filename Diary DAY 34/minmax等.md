![image-20220120000800640](C:\Users\73887\AppData\Roaming\Typora\typora-user-images\image-20220120000800640.png)
	

![image-20220120000859700](C:\Users\73887\AppData\Roaming\Typora\typora-user-images\image-20220120000859700.png)

+++



Min-Max

![image-20220120112742778](C:\Users\73887\AppData\Roaming\Typora\typora-user-images\image-20220120112742778.png)

![image-20220120112755451](C:\Users\73887\AppData\Roaming\Typora\typora-user-images\image-20220120112755451.png)

Min-Max标准化是指对原始数据x进行线性变换，将y值映射到[0，1]之间

```python
import numpy as np
import math

"""
around(arr,decimals=?)?maintain x decimals
"""

class DataNormalization:
    def __init__(self):
        self.arr = np.array([1,2,3,4,5,6,7,8,9])
        self.x_max = self.arr.max() 
        self.x_min = self.arr.min()
        self.x_mean = self.arr.mean()
        self.x_std = self.arr.std()

    def Min_MaxNorm(self):
        arr = np.around(((self.arr - self.x_min) / (self.x_max - self.x_min)), decimals = 4)
        print("Min_MaxNorm:{}".format(arr))

if __name__ == "__main__":
    a = DataNormalization()
    a.Min_MaxNorm()

```

```python
Min_MaxNorm:[0.    0.125 0.25  0.375 0.5   0.625 0.75  0.875 1.   ]
```

