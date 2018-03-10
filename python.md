# python人工智能

## python基础

### 条件表达式
```
if x > 0:
	x = math.sqrt(x)
else :
	x = flaot('nan')
等价于：
x = math.sqrt(x) if x >　0 else float('nan')
```
### 字典的遍历
```
dict = {'a': 1, 'b': 2, 'c': 3, 'd': 4}
只遍历键：
for key in dict.keys():
    print(key)
只遍历值：
for value in dict.values():
    print(value)
遍历键值：    
for key, value in dict.items():
    print('{}网址是{}'.format(key, value))
```
字典的变化： 
```
dic_key = {x.upper(): x*3 for x in 'abcd'}
    print(dic_key)
    
结果：{'A': 'aaa', 'B': 'bbb', 'C': 'ccc', 'D': 'ddd'}
```

### 列表的变化
初始：
```
    l1 = []
    for i in range(10):
        if i % 2 ==0:
            l1.append(i)
    print(l1)
```
等价于：
```
    l2 = [i for i in range(10) if i % 2 == 0]
    print(l2)
```


## 科学计算库Numpy as np

### 矩阵
ndarry，N维数组对象，用法是直接用变量去点调用打印输出  
`ndim`指的是维度的个数  
`shape`是打印或限定各维度的大小  
`dtype`数据类型  
例子
`x.ndim,x.shape(输出行列...)，`

初始化一个矩阵  
`np.zeros((3,2)),np.ones((4,5))`  
创建一个随机一维数组  
`np.arange(0,30,2)   0-30每隔两个数`  
将一维数组变成多维数组  
`n = n.reshape(3,5)` 将n变成三行五列  
### 矩阵的遍历
生成一个随机的矩阵
`t = np.random.randint(0,10,(4,3))`生成一个随机4行3列矩阵  
数组的行遍历：  
```
for row in t:
	print(t)
```
取到下标的数组遍历：  
```
for i,row in enumerate(t):
	print('row{}is{}'.format（i,row）)

```
### 数组的向量化
把数组看成一个对象  
例如对于一个数组`t1 =t2 * 2 `则把数组里面所有值乘2  
使用`zip`对两个数组进行遍历计算  :
```
for i, j in zip(t, t1):
	print('{}+{}={}'.format(i,j,i+j))
```
