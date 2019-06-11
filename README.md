# PCV_Assignment_11
graph cut test
## 图像分割
   所谓图像分割指的是根据灰度、颜色、纹理和形状等特征把图像划分成若干互不交迭的区域，并使这些特征在同一区域内呈现出相似性，而在不同区域间呈现出明显的差异性。  
## Graph Cut（图割）
  Graph cuts是一种十分有用和流行的能量优化算法，在计算机视觉领域普遍应用于前背景分割（Image segmentation）、立体视觉（stereo vision）、抠图（Image matting）等。  
  具体相关资料参考[这里](https://blog.csdn.net/kyjl888/article/details/78253829)  
  
## 过程
  原图：  
  ![emmmm]()
  源码：
```python
# -*- coding: utf-8 -*-

from scipy.misc import imresize
from PCV.tools import graphcut
from PIL import Image
from numpy import *
from pylab import *

im = array(Image.open("empire.jpg"))
im = imresize(im, 0.07)
size = im.shape[:2]
print ("OK!!")

# add two rectangular training regions
labels = zeros(size)
labels[3:18, 3:18] = -1
labels[-18:-3, -18:-3] = 1
print ("OK!!")


# create graph
g = graphcut.build_bayes_graph(im, labels, kappa=1)

# cut the graph
res = graphcut.cut_graph(g, size)
print ("OK!!")


figure()
graphcut.show_labeling(im, labels)

figure()
imshow(res)
gray()
axis('off')

show()
```
  结果输出：
```
OK!!
OK!!
est prob (2, 2184) range(0, 2)
OK!!
```
  分割后:  
  ![emmmm]()
