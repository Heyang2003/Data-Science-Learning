

Argparse与图片视频读取

Argparse用于读取用户在交互界面传递的信息。

```python
import argparse

parser = argparse.ArgumentParser(description='Process some integers.')
parser.add_argument('integers', metavar='N', type=int, nargs='+',
                    help='an integer for the accumulator')
parser.add_argument('--sum', dest='accumulate', action='store_const',
                    const=sum, default=max,
                    help='sum the integers (default: find the max)')

args = parser.parse_args()
print(args.accumulate(args.integers))


```

比如上面的是一个去最大值和求和的用户界面

![image-20220803164358513](C:\Users\He Yang\AppData\Roaming\Typora\typora-user-images\image-20220803164358513.png)

用户通过输入数字达到代码所实现的功能

opencv读取图片和视频

图片

```python
import numpy as np
import cv2
import argparse


ap = argparse.ArgumentParser()
ap.add_argument("-i","--input",required=True,help="path to input image")

args = vars(ap.parse_args())

img = cv2.imread(args["input"])




cv2.imshow('input', img)
k=cv2.waitKey(0)

if k == 27:
    cv2.destoryAllwindows()
elif k == ord("s"):
    cv2.imwrite("input",img)
    cv2.destoryallWindows()

```

视频

```python
import cv2
import argparse


ap = argparse.ArgumentParser()
ap.add_argument("-i","--input",required=True,help="path to input image")

args = vars(ap.parse_args())

capture = cv2.VideoCapture(args["input"])



ret,frame = capture.read()
while ret:
    
    cv2.imshow("input",frame)
    ret,frame = capture.read()
 
   
    if cv2.waitKey(20) & 0xff == ord('q'):
        break
 

capture.release()
 

cv2.destroyAllWindows()

```

环境设置：

图片和视频都是放在相同文件夹下使用

使用方法：

相关代码用py文件保存后，用安装opencv和Argparse的环境当中运行

调用方法：

```
python 文件名
```

