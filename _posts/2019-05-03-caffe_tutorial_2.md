---
layout:     post
title:      Caffe简明教程（二）
subtitle:   caffe的编译和安装
date:       2019-05-03
author:     何晨
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - 技术
    - 机器学习
---

接下来，我会就caffe的编译过程做一些简要的说明。 当然，你也可以创建一个caffe_installation.sh文件，复制这些命令到shell文件中，实现一键安装caffe。

#### 安装过程

~~~
# CAFFE INSTALLATION: http://caffe.berkeleyvision.org/installation.html

1. 安装必要组件
一共包含3种安装方式，1.1 - 通过 ubuntu 本地安装，1.2 - 通过 conda 安装，1.3 - 通过预编译的 caffe 文件安装。你可以选择其中一种适合你的方式来安装 caffe

1.1 通过 ubuntu 本地的 apt-get 安装
# install optional dependencies
# cuda, cudnn, opencv.

# Keep Ubuntu or Debian up to date
# 更新软件列表
sudo apt-get -y update
# 更新软件
sudo apt-get -y upgrade
sudo apt-get -y dist-upgrade
sudo apt-get -y autoremove

# Base packages
sudo apt-get install -y build-essential cmake git pkg-config

# DEPENDENCIES
# BLAS: 被广泛使用的线性代数库（ATLAS/MKL/OpenBLAS）
sudo apt-get install -y libopenblas-dev
sudo apt-get install -y libatlas-base-dev
# Google 开源的一套东西: protobuf: 数据序列化框架。gflags: 命令行参数解析库。glog: 日志记录框架
# caffe 的 layer 开发以 protobuf 作为格式
sudo apt-get install -y libprotobuf-dev protobuf-compiler
sudo apt-get install -y libgflags-dev
sudo apt-get install -y libgoogle-glog-dev
# Boost(>=1.55): 著名的 C++ 第三方库，Boost 虽然也能从软件源安装，但需要注意版本，如果版本过低还是需要进行编译安装。
sudo apt-get install --no-install-recommends libboost-all-dev

# OPTIONAL DEPENDENCIES
# OpenCV(>=2.4): 著名的计算机视觉库
# 1，下载源码包安装，(参考地址)[https://blog.csdn.net/yhaolpz/article/details/71375762]
# 2，利用自动脚本安装：(参考地址)[https://github.com/jayrambhia/Install-OpenCV]
# 3，直接从官方安装编译好的opencv库
sudo apt-get install -y libopencv-dev 

# IO 相关的库：hdf5, leveldb（leveldb需要snappy）, snappy, lmdb.
sudo apt-get install -y libhdf5-serial-dev
sudo apt-get install -y libleveldb-dev
sudo apt-get install -y libsnappy-dev
sudo apt-get install -y liblmdb-dev

# INTERFACES (Python 3)
sudo apt-get install -y python3-dev python3-numpy libboost-python-dev

1.2 通过 conda 安装 
# 我没有用 conda 创建新的环境，而是用的默认环境。
# 可以直接用conda安装依赖，（只要这些依赖在 ~/anaconda3/include，~/anaconda3/lib 里面，然后 conda 是添加到用户环境变量里面的，所以这些依赖可以覆盖系统的依赖 而被调用）
# hdf5, snappy 没有被安装，conda 里面包含了这两个包。安装完，我发现这些包都在 ~/anaconda3/lib 和 ~/anaconda3/include 里面，所以就没添加到用户环境变量。
conda install boost hdf5 snappy leveldb lmdb gflags glog

# 注意：protobuf不在 ~/anaconda3/include 目录下，而是 ~/anaconda3/pkgs/libprotobuf-3.5.2-h6f1eeef_0，所以需要添加到环境变量中。
protoc --version  # 查看系统protoc版本
conda install protobuf==3.5.1
echo 'export PATH=/home/shaoxiaowen/anaconda3/pkgs/libprotobuf-3.5.2-h6f1eeef_0/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/home/shaoxiaowen/anaconda3/pkgs/libprotobuf-3.5.2-h6f1eeef_0/lib:$LD_LI``BRARY_PATH' >> ~/.bashrc
source ~/.bashrc
protoc --version  # 查看当前protoc版本

# 到release页面下载和protoc（即protobuf-cpp）版本一样的protobuf-python，然后：
tar -xzvf protobuf-python-3.5.1.tar.gz
cd protobuf-python-3.5.1
cd python
python setup.py build
python setup.py test
python setup.py install

# 这样protobuf python runtime就编译和安装好了。
# 查看protobuf安装情况。
conda list | grep protobuf

# OpenBLAS
git clone https://github.com/xianyi/OpenBLAS.git
cd OpenBLAS
make FC=gfortran -j $(($(nproc) + 1))
make PREFIX=~/Openblas install
echo 'export LD_LIBRARY_PATH=/home/shaoxiaowen/Openblas/lib:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc

# OpenCV
# 关于OpenCV，我参考的那篇博客上已经其他很多文章里都是手动安装编译，这边我直接使用conda安装：
conda install -c menpo opencv3

1.3 安装预编译的 caffe
# 备注：我们亦可以安装预编译的 caffe 。(参考地址)[https://caffe.berkeleyvision.org/install_apt.html]
# For Ubuntu (>= 17.04)， Installing pre-compiled Caffe
# Everything including caffe itself is packaged in 17.04 and higher versions. To install pre-compiled Caffe package, just do it by
# for CPU-only version, or
sudo apt install caffe-cpu
# for GPU version
sudo apt install caffe-cuda

# 备注：我们亦可以通过 conda 安装预编译的 caffe
# conda create -n caffe-env pip python==3.6
# conda active caffe-env
# conda install caffe-gpu
# conda deactivate
# 安装完成，跳过以下步骤

2. caffe编译
# 上述依赖库都安装完成后，就可以编译caffe
git clone https://github.com/BVLC/caffe.git
cd caffe
# 然后进入Python 目录安装依赖关系：
cd /path/to/caffe/python
# use python3 by default
for req in $(cat requirements.txt); do sudo -H pip3 install $req --upgrade; done
# back to caffe root repo
cd ..

# 修改 caffe 目录下的 Makefile 文件。参考我的上一篇教程
vim Makefile

# 修改 caffe 目录下的 Makefile.config 文件。参考我的上一篇教程
# cp Makefile.config.example Makefile.config
# vim Makefile.config  # Adjust Makefile.config (for example, if using Anaconda Python)

# 编译
# 如果之前编译过的话，清除掉之前编译的内容
make clean
# j8是使用8个线程，看计算机CPU有几个内核
make all -j $(($(nproc) + 1))
# 如果之前的配置或安装出错，那么编译就会出现各种各样的问题，所以前面的步骤一定要细心。
# 编译成功后可运行测试：
make test -j $(($(nproc) + 1))
make runtest -j $(($(nproc) + 1))
make pycaffe -j $(($(nproc) + 1))

# optional
# make distribute

# compile matlab interface
# make all matcaffe
# make mattest

3. 导入 caffe
方法一（将 pycaffe 加入系统环境变量）
sudo gedit  ~/.bashrc
# add following 2 lines
export CAFFE_ROOT="/path/to/caffe":$CAFE_ROOT
export PYTHONPATH="/path/to/caffe/python:$PYTHONPATH":$PYTHONPATH
# validate the modification
source ~/.bashrc

方法二（通过绝对路径调用 pycaffe API）
import sys
caffe_root = '/path/to/caffe'
sys.path.insert(0, caffe_root + 'python')
or:
sys.path.append('/path/to/caffe/python')

4. 验证 caffe 安装
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
安装低版本gcc和g++，并创建链接（我采用的方案），或注释掉错误代码（不推荐），或更改gcc各版本的优先级（请自行百度）。

方法一
此处为以后考虑安装了gcc-6和g++-6,大家可以自行决定版本，只要比错误中提到的gcc版本支持上限小就没问题
sudo apt-get install gcc-6
sudo apt-get install g++-6
创建软链接：
sudo ln -s /usr/bin/gcc-6 /usr/local/cuda/bin/gcc
sudo ln -s /usr/bin/g++-6 /usr/local/cuda/bin/g++

方法二（不推荐）
sudo gedit /usr/local/cuda/include/host_config.h
将
#error-- unsupported GNU version! gcc versions later than 6 are not supported!
改为
//#error-- unsupported GNU version! gcc versions later than 6 are not supported!


3. Err3

F0419 21:47:59.244611 23517 layer_factory.hpp:81] Check failed: registry.count(type) == 1 (0 vs. 1) Unknown layer type: AutoCrop (known types: AbsVal, Accuracy, ArgMax, BNLL, BatchNorm, BatchReindex, Bias, Concat, ContrastiveLoss, Convolution, Crop, Data, Deconvolution, Dropout, DummyData, ELU, Eltwise, Embed, EuclideanLoss, Exp, Filter, Flatten, HDF5Data, HDF5Output, HingeLoss, Im2col, ImageData, InfogainLoss, InnerProduct, Input, LRN, LSTM, LSTMUnit, Log, MVN, MemoryData, MultinomialLogisticLoss, PReLU, Parameter, Pooling, Power, Python, RNN, ReLU, Reduction, Reshape, SPP, Scale, Sigmoid, SigmoidCrossEntropyLoss, Silence, Slice, Softmax, SoftmaxWithLoss, Split, TanH, Threshold, Tile, WindowData)
Unknown layer type: AutoCrop
原因：如果使用UCLA版本（https://github.com/BVLC/caffe）的标准版caffe,会导致以上问题。此project中，作者自行加入了一些组件（自定义层）。 
解决方案：
编译并安装正确的caffe版本
~~~

