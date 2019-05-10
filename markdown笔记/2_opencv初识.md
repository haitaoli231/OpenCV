# 一.图片的读取和显示

```python
# 1.引入模块
import cv2 as cv
# 2.读取图片
img = cv.imread('../sources/cat.jpg', 1)	# imread() -- 参数一:图片路径  参数二:0指gray,1指color
# 3.创建窗体,显示图片
cv.imshow('Image', img)	# 'Image'指窗体名称, img是上面读取出来的图片数据

# 4.保持窗体存在,直到手动关闭
cv.waitKey(0)
# 5.销毁所有窗体
cv.destoryAllWindows()
```



# 二.图像质量和图片的写入

事实上, 图像的读取和显示经历了这样几个步骤:

文件读取 --> 对文件的封装格式进行解析 --> 数据解码 --> 数据加载

而 opencv内部代码已经帮我们做了2和3两步, 所以在代码层面上, 我们只看到了 图像读取和图像显示(图像加载)这两步.

在写入图像的过程中, opencv会对图像进行压缩, jpg与png差别如下:

|      jpg格式      |     png格式     |
| :---------------: | :-------------: |
|     有损压缩      |    无损压缩     |
| 压缩比范围: 0~100 | 压缩比范围: 0~9 |

```python
import cv2 as cv

# 读取图像
img = cv.imread('../sources/cat.jpg', 1)
# 写入jpg格式图像: 压缩比范围0~100
cv.imwrite('../sources/cat_jpg.jpg', img, [cv.IMWRITE_JPEG_QUALITY, 50])	# [] 里面第一个参数就是压缩比类型,第二个参数是压缩比数值
```

```python
import cv2 as cv

# 读取图像
img = cv.imread('../sources/cat.jpg', 1)
# 写入png格式图像: 压缩比范围0~9
cv.imwrite('../sources/cat_png.png', img, [cv.IMWRITE_PNG_COMPRESSION, 0])	# [] 里面第一个参数就是压缩比类型,第二个参数是压缩比数值
```



# 三.像素操作和像素读取

- **颜色通道**: RGB, BGR
  - RGB表示三个颜色通道, 分别为: R, G, B
  - R表示red, G表示green, B表示blue



- **宽高**: 图片在水平方向上和竖直方向上有多少个像素点
- **像素**: 图片上的每一个小方块就表示一个像素点
- **颜色通道**: 每个颜色通道的颜色深度是 8bit 表明该颜色通道可以表示的颜色范围在0~255之间
  - 每一个像素点由RGB三个颜色通道组成, 若每一个颜色通道的深度都是 8bit, 则一个像素点有 256^3 种表示方式, 一个像素的大小是 3*8bit



- **图片大小**:
  - 假设一个图片的宽高是 640*480, 颜色深度是 8bit, 那么该图片的大小是:
  - `640*480*3*8bit=7372800bit=921600bytes=900KB`
  - 注意: 1byte=8bit
- 对于png图片而言, 不仅有RGB属性还有一个alpha透明度属性



```python
import cv2 as cv

# 读取图像
img = cv.imread('../sources/cat.jpg', 1)

# 找到图像中坐标为[100, 100]对应的像素点的 b, g, r
(b, g, r) = img[100, 100]	# 注意: imread()读取出来的数据是BGR,而不是RGB!


# 要求如下: 以[10, 100]为起点,[110, 100]为终点, 在图片上画出一条(b, g, r)=(255, 0, 0)的直线
for i in range(1, 101):
    img[10 + i, 100] = (255, 0, 0)
cv.imshow('Image', img)		# 'Image'指窗体名称
cv.waitKey(0)
cv.destroyAllWindows()
```

