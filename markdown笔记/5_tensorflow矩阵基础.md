# 一.关于feed_dict参数

```python
import tensorflow as tf

# 使用placeholder创建张量
data1 = tf.placeholder(tf.float32)
data2 = tf.placeholder(tf.float32)

dataAdd = tf.add(data1, data2)

with tf.Session() as sess:
    # run()的第一个参数是op,第二个参数是张量对应的具体数据
    print(sess.run(dataAdd, feed_dict={data1:6, data2:2}))
print('end!')
```



# 二.矩阵的组成

- 什么是矩阵?
    - 类比法: 可以把矩阵看作是一个数组. 若矩阵是M行N列,那么数组中就会嵌套有M个子数组,每一个子数组中有N个数据. 子数组与子数组之间,数据与数据之间均用逗号隔开.

- 如何表示矩阵的行和列?
    - 查看矩阵data第0行的所有数据: data[0]
    - 查看矩阵data第0列的所有数据: data[:,0]


- 如何表示矩阵中的每一个数据?
    - 查看矩阵data第0行第0列对应的数据: data[0,0]
    - 查看矩阵data第1行第1列对应的数据: data[1,1]



```python
import tensorflow as tf

# 维度:(1,2)
data1 = tf.constant([[6, 6]])
# 维度:(2,1)
data2 = tf.constant([[2],
                     [2]])
# 维度:(1,2)
data3 = tf.constant([[3, 3]])
# 维度:(3,2)
data4 = tf.constant([[1, 2],
                     [3, 4],
                     [5, 6]])

print(data4.shape)	# shape可以查看矩阵的维度

with tf.Session() as sess:
    print(sess.run(data4))
    print(sess.run(data4[0])) # data4的第0行
    print(sess.run(data4[:,0]))	# data4的第0列
    print(sess.run(data4[1,1])) # data4第1行第1列对应的数字
    
'''执行结果:
(3, 2)
[[1 2]
 [3 4]
 [5 6]]
[1 2]
[1 3 5]
4
'''
```



# 三.矩阵的运算

矩阵相加: M×N + M×N

矩阵相乘: M×k * k×N

```python
import tensorflow as tf

data1 = tf.constant([[6, 6]])
data2 = tf.constant([[2],
                     [2]])
data3 = tf.constant([[3, 3]])
data4 = tf.constant([[1, 2],
                     [3, 4],
                     [5, 6]])

matAdd = tf.add(data1, data3)		# 矩阵相加
matMul = tf.matmul(data1, data2)	# 矩阵相乘
matMul2 = tf.multiply(data1, data2)	# 普通乘法

with tf.Session() as sess:
   	print(sess.run(matAdd))
    print(sess.run(matMul))
    print(sess.run(matMul2))
    
    print(sess.run([matAdd, matMul]))	# 一个会话同时执行多个计算图
```



# 四.矩阵的创建

```python
tf.constant()		# 自定义矩阵
tf.zeros()			# 全0矩阵
tf.ones()			# 全1矩阵
tf.fill()			# 填充矩阵
tf.zeros_like()		# 相似
tf.linespace()		# 等分
tf.random_uniform()	# 随机
```

```python
import tensorflow as tf

# 自定义矩阵
mat0 = tf.constant([[1, 2, 3],[4, 5, 6]])
# 全0矩阵
mat1 = tf.zeros([2, 3])
# 全1矩阵
mat2 = tf.ones([2, 3])
# 填充矩阵
mat3 = tf.fill([2, 3], 99)

with tf.Session() as sess:
    print(sess.run(mat1), end='\n\n')
    print(sess.run(mat2), end='\n\n')
    print(sess.run(mat3), end='\n\n')


'''执行结果:
[[0. 0. 0.]
 [0. 0. 0.]]

[[1. 1. 1.]
 [1. 1. 1.]]

[[99 99 99]
 [99 99 99]]
'''
```

```python
import tensorflow as tf

mat0 = tf.constant([[1, 2, 3],[4, 5, 6]])
mat1 = tf.zeros_like(mat0)
mat2 = tf.linspace(0.0, 2.0, 11)
mat3 = tf.random_uniform([2, 3], -1, 2)

with tf.Session() as sess:
    print(sess.run(mat1), end='\n\n')
    print(sess.run(mat2), end='\n\n')
    print(sess.run(mat3), end='\n\n')
    
    
'''执行结果:
[[0 0 0]
 [0 0 0]]

[0.        0.2       0.4       0.6       0.8       1.        1.2
 1.4       1.6       1.8000001 2.       ]

[[ 1.4726727  -0.12585771  1.3514347 ]
 [ 0.89253664 -0.7657509  -0.41237807]]
'''
```

