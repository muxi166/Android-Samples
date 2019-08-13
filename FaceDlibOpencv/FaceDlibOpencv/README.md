# FaceDlibOpencv
本项目基于 [OpenCV](https://opencv.org) 和 [Dlib](http://dlib.net) 的图片、视频人脸检测和人脸识别，同时也集成了虹软的ArcFace。

> 如果github同步慢，也可以到 https://gitee.com/dengly/FaceDlibOpencv 同步。

## 版本
* [OpenCV 3.4.1](https://opencv.org/opencv-3-4-1.html) 的 Android SDK
* [Dlib 19.10](http://dlib.net/files/dlib-19.10.tar.bz2)
* [虹软 ArcFace v1.1](http://www.arcsoft.com.cn/ai/arcface.html) 的 Android SDK

## 说明
* 算法模型存放在SD卡的```model```文件夹下，可以通过修改```com.zzwtec.facedlibopencv.Constants```
* 人脸库存放在SD卡的```faces```文件夹下，可以通过修改```com.zzwtec.facedlibopencv.Constants```
* 目前 OpenCV 只是用于摄像头的管理和显示，人脸检测、特征标记、识别都是使用 Dlib
* 经测试 Dlib 的人脸特征提取耗时比较大，如在锤子的[坚果手机 U1](https://www.smartisan.com/jianguo/#/specs)上，原图是1280x960，经压缩处理是320x240,一次人脸检测耗时是280毫秒左右，一次一个人脸特征提取耗时是6800毫秒左右，一次人脸特征比对耗时是0.03毫秒左右
* 在处理屏幕旋转和摄像头图像旋转时，发现 Dlib 对人脸方向和屏幕方向不一致时检测不到人脸，而虹软 ArcFace 会自动处理这个问题，并在返回结果在存有人脸方向

## 测试结果

> 原图是1280x960，经压缩处理是320x240

#### Dlib测试结果

机型	| 一次人脸检测耗时 | 一次一个人脸特征提取耗时 | 一次人脸特征比对耗时
:---: | :---: | :---: | :---:
坚果 U1 | 280毫秒左右 | 6800毫秒左右 | 0.03毫秒左右
坚果 pro2 | 93毫秒左右 | 1060毫秒左右 | 0.002毫秒左右

#### 虹软测试结果
机型	| 一次人脸检测耗时 | 一次一个人脸特征提取耗时 | 一次人脸特征比对耗时
:---: | :---: | :---: | :---:
坚果 U1 | 43毫秒左右 | 943毫秒左右 | 0.883毫秒左右
坚果 pro2 | 20毫秒左右 | 314毫秒左右 | 0.308毫秒左右

经测试发现虹软的压缩和不压缩图片，效果是差不多的，以下是在坚果 U1上测试的结果

* 压缩： 320x240
* 虹软 facedetection time: 43.425364 ms
* 虹软 人脸特征提取 time: 943.762292 ms
* 虹软 人脸特征比对 time: 0.883125 ms
* Score:0.69143975

* 不压缩： 1280x960
* 虹软 facedetection time: 46.223854 ms
* 虹软 人脸特征提取 time: 1067.310573 ms
* 虹软 人脸特征比对 time: 1.104636 ms
* Score:0.62367505

#### 坚果 U1 项目对比
项目 | 人脸检测+人脸特征提取 | 一次人脸特征比对 | 总耗时
:---: | :---: | :---: | :---:
Dlib | 7080毫秒左右 | 0.03毫秒左右 | 7080.03毫秒左右
虹软 | 986毫秒左右 | 0.883毫秒左右 | 986.883毫秒左右

> * 从这个结果可以看出Dlib和虹软各有优缺点
> * 如果当比对次数大于 7144 次后，Dlib更有优势
> * 如果当比对次数小于 7144 次，虹软更有优势

#### 坚果 pro2 项目对比
项目 | 人脸检测+人脸特征提取 | 一次人脸特征比对 | 总耗时
:---: | :---: | :---: | :---:
Dlib | 1153毫秒左右 | 0.002毫秒左右 | 1153.002毫秒左右
虹软 | 334毫秒左右 | 0.308毫秒左右 | 334.308毫秒左右

> * 从这个结果可以看出Dlib和虹软各有优缺点
> * 如果当比对次数大于 2676 次后，Dlib更有优势
> * 如果当比对次数小于 2676 次，虹软更有优势

#### 全志R58芯片测试结果
机型	| 一次人脸检测耗时 | 一次一个人脸特征提取耗时 | 一次人脸特征比对耗时
:---: | :---: | :---: | :---:
Dlib | 277毫秒左右 | 6624毫秒左右 | 0.005毫秒左右
虹软 | 51毫秒左右 | 2470毫秒左右 | 1.401毫秒左右

> * 原图是640x480 压缩： 320x240
> * 从这个结果可以看出Dlib和虹软各有优缺点
> * 如果当比对次数大于 3137 次后，Dlib更有优势
> * 如果当比对次数小于 3137 次，虹软更有优势

###### 备注
欢迎大家将测试结果通过邮件发送到 971257255@qq.com ，格式可以参考上面的。