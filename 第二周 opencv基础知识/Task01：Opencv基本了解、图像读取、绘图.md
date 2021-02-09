# Task01：Opencv基本了解、图像读取、绘图

## 思考题

#### 1. Opencv库与Matlab、halcon的区别？

HALCON与OpenCV都是函数库，都提供了多种编程语言访问的接口。不同在于：

1. HALCON可以用C，C++，C#，Visual basic和Delphi等语言访问，OpenCV提供了Python、Ruby、MATLAB等语言的接口。
2. OpenCV侧重计算机视觉领域，HALCON侧重机器视觉领域。
3. HALCON是商业软件，而OpenCV可以在商业和研究领域中免费使用。

虽然MATLAB也带有很多函数库，但不同于HALCON和OpenCV，MATLAB是个完整的集成开发环境，包括了编辑器、函数库、还有Matlab语言本身均由MathWorks公司提供。例如，用MATLAB你可以debug，但是对于OpenCV相关的代码调试，你就需要Visual Studio了

#### 2. 为什么是import **cv2**？

实际上，”cv2”中的”2”并不表示OpenCV的版本号。我们知道，OpenCV是基于C/C++的，”cv”和”cv2”表示的是底层C API和C++API的区别，”cv2”表示使用的是C++API。这主要是一个历史遗留问题，是为了保持向后兼容性。

#### 3. 在显示完之后，用不用cv.destroyWindow()有什么区别？

根据 [官方文档](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html?highlight=destroyallwindows) ：

> You can call [`destroyWindow()`](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html?highlight=destroyallwindows#void destroyWindow(const string& winname)) or [`destroyAllWindows()`](https://docs.opencv.org/2.4/modules/highgui/doc/user_interface.html?highlight=destroyallwindows#void destroyAllWindows()) to close the window and de-allocate any associated memory usage. For a simple program, you do not really have to call these functions because all the resources and windows of the application are closed automatically by the operating system upon exit.

您可以调用destroyWindow()或destroyAllWindows()来关闭窗口并取消分配任何相关的内存使用。对于一个简单的程序，您实际上不必调用这些函数，因为应用程序的所有资源和窗口都会在退出时由操作系统自动关闭。

#### 4. png图片格式和jpg图片格式有什么区别？

png无损压缩，支持透明；jpg有损压缩，不支持透明。

## 练习题

#### 1. 同时显示两张不同分辨率的图片，对比他们的大小

```python
import cv2 as cv

img1 = cv.imread("awesomeface1.png")
img2 = cv.imread("awesomeface2.png")
cv.imshow("1", img1)
cv.imshow("2", img2)
print(img1.shape)
print(img2.shape)
cv.waitKey(0)
cv.destroyAllWindows()
```

![image-20210209143805558](Robomaster\第二周 opencv基础知识\Task01：Opencv基本了解、图像读取、绘图.assets\image-20210209143805558.png)

#### 2. 使用Opencv，测试一下你电脑摄像头的分辨率和帧率是多少

```python
import cv2 as cv

cap = cv.VideoCapture(0)
if not cap.isOpened():
    print("Cannot open camera")
    exit()
else:
    print(cap.get(cv.CAP_PROP_FPS))
    print(cap.get(cv.CAP_PROP_FRAME_WIDTH), cap.get(cv.CAP_PROP_FRAME_HEIGHT))
while True:
    ret, frame = cap.read()
    if not ret:
        print("Can't receive frame (stream end?). Exiting ...")
        break
    # Display the resulting frame
    cv.imshow('frame', frame)
    if cv.waitKey(1) == ord('q'):
        break
# When everything done, release the capture
cap.release()
cv.destroyAllWindows()
```

![image-20210209200248209](Robomaster\第二周 opencv基础知识\Task01：Opencv基本了解、图像读取、绘图.assets\image-20210209200248209.png)

#### 3. 利用电脑摄像头从外界拍摄一幅自己的图像，添加圆（或其他图形）给自己打码，图片右下角添加自己的网名和时间。

```python
import time
import cv2 as cv

cap = cv.VideoCapture(0)
if not cap.isOpened():
    print("Cannot open camera")
    exit()
ret, frame = cap.read()
cap.release()
if not ret:
    print("Can't receive frame (stream end?). Exiting ...")
    exit()
cv.circle(frame, (347, 263), 80, (255, 255, 255), -1)
cv.putText(frame, 'wyz ' + time.asctime(time.localtime(time.time())), (350, 450), cv.FONT_HERSHEY_SIMPLEX, 0.5,
           (255, 255, 255))
cv.imshow('frame', frame)
cv.waitKey(0)
cv.destroyAllWindows()
```

![image-20210209202609433](Robomaster\第二周 opencv基础知识\Task01：Opencv基本了解、图像读取、绘图.assets\image-20210209202609433.png)
