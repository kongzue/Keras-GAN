## 关于此项目

请注意本库不接受 issues，仅用作记录跑起来 Keras-GAN 过程中遇到的一些问题及解决方法。

本次主要目的是跑起来其中的 CGAN，其他的项目遇到的问题类似，希望能对你有所帮助。

原库使用方法和提交 issues 请访问：[eriklindernoren/Keras-GAN](https://github.com/eriklindernoren/Keras-GAN)

## 关于运行Keras-GAN的几个问题记录

记录者 @kongzue

1. 需要keras-contrib，但是keras-contrib在官方仓库没有编译好的，需要手动拉取编译，方法是前往https://github.com/keras-team/keras-contrib.git下载到本地后

   ```
   git clone https://www.github.com/keras-team/keras-contrib.git
   cd keras-contrib
   python setup.py install
   ```

2. ~~Git相关，其一是配置全局代理：~~

   ```
   git config --global https.proxy http://127.0.0.1:1080
   git config --global https.proxy https://127.0.0.1:1080
   ```

   其次是配置禁用 SSL 验证

   ```
   git config --global http.sslVerify “false”
   ```

3. tensorflow必须在python3.6以下安装，我的环境是Python3.6

![image](https://user-images.githubusercontent.com/10115359/190047588-7450e492-917d-4f9c-bc42-9eb87783049c.png)

4. 会遇到无法连接到亚马逊服务器amazonaws.com

   需要手动下载 mnist.npz

   ```
   https://s3.amazonaws.com/img-datasets/mnist.npz
   ```

   全局搜索（双击shift）："minst.load_data"

![image](https://user-images.githubusercontent.com/10115359/190047608-1b086e3c-a9b7-4c80-b6f7-0954a79e75fb.png)

 然后找到并修改其 path 信息，系统提示只读的话选择强行修改：

![image](https://user-images.githubusercontent.com/10115359/190047626-00b32217-9a87-4338-9867-135c0e21a08b.png)

指向你刚刚下载的mnist.npz文件

5. 遇到错误：tensorflow.python.framework.errors_impl.FailedPreconditionError: Error while...

   需要修改代码

![image](https://user-images.githubusercontent.com/10115359/190047654-6c4b807c-b153-4b67-8a1a-a284956934d1.png)

由原来的

```python
from keras.optimizers import Adam
```

改为：

```python
from tensorflow.keras.optimizers import Adam
```

6. 运行成功。

![image](https://user-images.githubusercontent.com/10115359/190047671-b7325556-bb09-434f-84fa-6102d8d32205.png)
