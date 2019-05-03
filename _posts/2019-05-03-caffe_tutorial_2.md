---
layout:     post
title:      Caffe简明教程（一）
subtitle:   caffe的编译和安装
date:       2019-05-03
author:     何晨
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - 技术
    - 机器学习
---

接下来，我会就caffe的编译过程做一些简要的说明。 当然，你也可以创建一个caffe_installation.sh文件，复制这些命令到shell文件中，实现一键安装caffe

#### 安装过程

~~~
# CAFFE INSTALLATION: http://caffe.berkeleyvision.org/installation.html

1. 安装必要组件
# install optional dependencies
# cuda, cudnn, opencv.

# Keep Ubuntu or Debian up to date
sudo apt-get -y update
sudo apt-get -y upgrade
sudo apt-get -y dist-upgrade
sudo apt-get -y autoremove

# Base packages
sudo apt-get install -y build-essential cmake git pkg-config

# DEPENDENCIES
sudo apt-get install -y libopenblas-dev
sudo apt-get install -y libatlas-base-dev
sudo apt-get install -y libprotobuf-dev protobuf-compiler
sudo apt-get install -y libhdf5-serial-dev
sudo apt-get install -y libgflags-dev
sudo apt-get install -y libgoogle-glog-dev
sudo apt-get install --no-install-recommends libboost-all-dev

# OPTIONAL DEPENDENCIES
# Install OpenCV 
sudo apt-get install -y libopencv-dev 
sudo apt-get install -y liblmdb-dev
sudo apt-get install -y libleveldb-dev
sudo apt-get install -y libsnappy-dev

# INTERFACES (Python 3)
sudo apt-get install -y python3-dev python3-numpy libboost-python-dev

# CLONING
git clone https://github.com/BVLC/caffe.git
cd caffe


2. 然后进入Python目录安装依赖关系：
cd /path/to/caffe/python
# use python3 by default
for req in $(cat requirements.txt); do sudo -H pip3 install $req --upgrade; done
# back to caffe root repo
cd ..

3. 修改 caffe 目录下的 Makefile 文件。参考我的上一篇教程

4. 修改 caffe 目录下的makefile.config。参考我的上一篇教程
# cp Makefile.config.example Makefile.config
# Adjust Makefile.config (for example, if using Anaconda Python)

5. 编译
make all -j $(($(nproc) + 1))
这是如果之前的配置或安装出错，那么编译就会出现各种各样的问题，所以前面的步骤一定要细心。
编译成功后可运行测试：
make test -j $(($(nproc) + 1))
make pycaffe -j $(($(nproc) + 1))
make runtest -j $(($(nproc) + 1))
# compile matlab interface
# make all matcaffe
# make mattest

8. 导入caffe
方法一（将 pycaffe 加入系统环境变量）
sudo gedit  ~/.bashrc
# add following 2 lines
export CAFFE_ROOT="/path/to/caffe":$CAFE_ROOT
export PYTHONPATH="/path/to/caffe/python:$PYTHONPATH":$PYTHONPATH
# validate the modification
source ~/.bashrc

方法二（通过绝对路径调用 pycaffe API）
caffe_root = '/home/charles/Workspace/contour_detection/RCF/rcf/examples'
import sys
sys.path.insert(0, caffe_root + 'python')
import caffe

7. 验证
编译 pycaffe 成功后，验证一下是否可以在 python 中导入 caffe 包，首先进入 python 环境：
your-pc$ python
>>> import caffe
~~~

#### 常见错误及解决方法
~~~
1. Err1

Error ./include/caffe/util/cudnn.hpp: In function ‘void caffe::cudnn::setConvolutionDesc(cudnnConvolutionStruct**, cudnnTensorDescriptor_t, cudnnFilterDescriptor_t, int, int, int, int)’:
原因：计算机中的Cudnn版本太新，而当前版本的caffe的cudnn实现与系统所安装的cudnn的版本不一致引起该错误。
参考： https://github.com/BVLC/caffe/issues/5793
解决方案：
将./include/caffe/util/cudnn.hpp 换成最新版的caffe里的cudnn的实现，即相应的cudnn.hpp。using: cp /path/to/caffe/include/caffe/util/cudnn.hpp ./include/caffe/util/
将./include/caffe/layers里的，所有以cudnn开头的文件，例如cudnn_conv_layer.hpp，都替换成最新版的caffe里的相应的同名文件。
将./src/caffe/layer里的，所有以cudnn开头的文件，例如cudnn_lrn_layer.cu，cudnn_pooling_layer.cpp，cudnn_sigmoid_layer.cu，都替换成最新版的caffe里的相应的同名文件。

2. Err2

error: #error -- unsupported GNU version! gcc versions later than 6 are not supported!
原因： ubuntu18.04默认使用gcc7, g++7，但是caffe不支持该版本的gcc, g++
解决方案：
安装低版本gcc和g++，并创建链接（我采用的方案）或更改gcc各版本的优先级（请自行百度）。
此处为以后考虑安装了gcc-6和g++-6,大家可以自行决定版本，只要比错误中提到的gcc版本支持上限小就没问题
sudo apt-get install gcc-6
sudo apt-get install g++-6
创建软链接：
sudo ln -s /usr/bin/gcc-6 /usr/local/cuda/bin/gcc
sudo ln -s /usr/bin/g++-6 /usr/local/cuda/bin/g++

3. Err3

F0419 21:47:59.244611 23517 layer_factory.hpp:81] Check failed: registry.count(type) == 1 (0 vs. 1) Unknown layer type: AutoCrop (known types: AbsVal, Accuracy, ArgMax, BNLL, BatchNorm, BatchReindex, Bias, Concat, ContrastiveLoss, Convolution, Crop, Data, Deconvolution, Dropout, DummyData, ELU, Eltwise, Embed, EuclideanLoss, Exp, Filter, Flatten, HDF5Data, HDF5Output, HingeLoss, Im2col, ImageData, InfogainLoss, InnerProduct, Input, LRN, LSTM, LSTMUnit, Log, MVN, MemoryData, MultinomialLogisticLoss, PReLU, Parameter, Pooling, Power, Python, RNN, ReLU, Reduction, Reshape, SPP, Scale, Sigmoid, SigmoidCrossEntropyLoss, Silence, Slice, Softmax, SoftmaxWithLoss, Split, TanH, Threshold, Tile, WindowData)
Unknown layer type: AutoCrop
原因：如果使用UCLA版本（https://github.com/BVLC/caffe）的标准版caffe,会导致以上问题。此project中，作者自行加入了一些组件（自定义层）。 
解决方案：
编译并安装正确的caffe版本
~~~

