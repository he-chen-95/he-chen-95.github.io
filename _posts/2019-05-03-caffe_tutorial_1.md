---
layout:     post
title:      Caffe简明教程（一）
subtitle:   caffe配置文件详解
date:       2019-05-03
author:     何晨
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - 技术
    - 机器学习
---

最近由于项目的需要开始研究和使用caffe框架。由于我也只是初学者，文中难免会有纰漏，欢迎大家指出。你可以在下方留言，我会尽量改正错误。
下面针对 makefile.config 文件以及 makefile 文件的配置做进一步说明。

#### makefile.config 文件配置详解
~~~
## Refer to http://caffe.berkeleyvision.org/installation.html
# Contributions simplifying and improving our build system are welcome!

# cuDNN acceleration switch (uncomment to build with cuDNN).
# "CuDNN是NVIDIA专门针对Deep Learning框架设计的一套GPU计算加速库"
USE_CUDNN := 1

# CPU-only switch (uncomment to build without GPU support).
# CPU_ONLY := 1

# uncomment to disable IO dependencies and corresponding data layers
# "因为要用到OpenCV库所以要打开"
USE_OPENCV := 1
# USE_LEVELDB := 0
# USE_LMDB := 0

# uncomment to allow MDB_NOLOCK when reading LMDB files (only if necessary)
#	You should not set this flag if you will be reading LMDBs with any
#	possibility of simultaneous read and write
# "当需要读取LMDB文件时可以取消注释，默认不打开。"
# ALLOW_LMDB_NOLOCK := 1

# Uncomment if you're using OpenCV 3
# "用pkg-config --modversion opencv命令查看opencv版本。"
OPENCV_VERSION := 3

# To customize your choice of compiler, uncomment and set the following.
# N.B. the default for Linux is g++ and the default for OSX is clang++
# CUSTOM_CXX := g++

# CUDA directory contains bin/ and lib/ directories that we need.
# "CUDA的安装目录"
CUDA_DIR := /usr/local/cuda

# On Ubuntu 14.04, if cuda tools are installed via
# "sudo apt-get install nvidia-cuda-toolkit" then use this instead:
# CUDA_DIR := /usr

# CUDA architecture setting: going with all of them.
# For CUDA < 6.0, comment the *_50 through *_61 lines for compatibility.
# For CUDA < 8.0, comment the *_60 and *_61 lines for compatibility.
# For CUDA >= 9.0, comment the *_20 and *_21 lines for compatibility.
# "这些参数需要根据GPU的计算能力选择"

CUDA_ARCH := -gencode arch=compute_30,code=sm_30 \
		-gencode arch=compute_35,code=sm_35 \
		-gencode arch=compute_50,code=sm_50 \
		-gencode arch=compute_52,code=sm_52 \
		-gencode arch=compute_60,code=sm_60 \
		-gencode arch=compute_61,code=sm_61 \
                -gencode arch=compute_61,code=compute_61

# BLAS choice:
# atlas for ATLAS (default)
# mkl for MKL
# open for OpenBlas
# "如果用的是ATLAS计算库则赋值atlas，MKL计算库则用mkl赋值，OpenBlas则赋值open。"
BLAS := atlas

# Custom (MKL/ATLAS/OpenBLAS) include and lib directories.
# Leave commented to accept the defaults for your choice of BLAS
# (which should work)!
# "blas库安装目录"
# BLAS_INCLUDE := /path/to/your/blas
# BLAS_LIB := /path/to/your/blas

# Homebrew puts openblas in a directory that is not on the standard search path
# "atlas库安装目录"
# "如果不是安装在标准路径则要指明"
# BLAS_INCLUDE := $(shell brew --prefix openblas)/include
# BLAS_LIB := $(shell brew --prefix openblas)/lib

# This is required only if you will compile the matlab interface.
# MATLAB directory should contain the mex binary in /bin.
# "matlab安装库的目录"
# MATLAB_DIR := /usr/local
# MATLAB_DIR := /Applications/MATLAB_R2012b.app

# NOTE: this is required only if you will compile the python interface.
# We need to be able to find Python.h and numpy/arrayobject.h.
# "python安装目录"

# PYTHON_INCLUDE := /usr/include/python2.7 \
# 		/usr/lib/python2.7/dist-packages/numpy/core/include

# Anaconda Python distribution is quite popular. Include path:
# Verify anaconda location, sometimes it's in root.
# ANACONDA_HOME := $(HOME)/anaconda
# PYTHON_INCLUDE := $(ANACONDA_HOME)/include \
		# $(ANACONDA_HOME)/include/python2.7 \
		# $(ANACONDA_HOME)/lib/python2.7/site-packages/numpy/core/include \

# ANACONDA_HOME := $(HOME)/Software/anaconda3
# PYTHON_INCLUDE := $(ANACONDA_HOME)/envs/rcf-conda/include \
# 		  $(ANACONDA_HOME)/envs/rcf-conda/include/python3.6m \
# 		  $(ANACONDA_HOME)/envs/rcf-conda/lib/python3.6/site-packages/numpy/core/include \

# Uncomment to use Python 3 (default is Python 2)
# "这两个文件在/usr/lib/x86_64-linux-gnu/目录下，名为libboost_python36.so和libpython3.6m.so，如果不是这两个名字，相应修改"
PYTHON_LIBRARIES := boost_python3 python3.6m
PYTHON_INCLUDE := /usr/include/python3.6m \
                 /usr/lib/python3/dist-packages/numpy/core/include

# We need to be able to find libpythonX.X.so or .dylib.
# "python库位置"

PYTHON_LIB := /usr/lib
# PYTHON_LIB := $(ANACONDA_HOME)/envs/rcf-conda/lib

# Homebrew installs numpy in a non standard path (keg only)
# PYTHON_INCLUDE += $(dir $(shell python -c 'import numpy.core; print(numpy.core.__file__)'))/include
# PYTHON_LIB += $(shell brew --prefix numpy)/lib

# Uncomment to support layers written in Python (will link against Python libs)
WITH_PYTHON_LAYER := 1

# Whatever else you find you need goes here.
# "Caffe在编译时，会按照MakeFile.config里面的INCLUDE_DIRS和LIBRARY_DIRS寻找要包含的头文件和需要链接的库文件。"
# INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include
# LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu /usr/lib/x86_64-linux-gnu/hdf5/serial

# If Homebrew is installed at a non standard location (for example your home directory) and you use it for general dependencies
# INCLUDE_DIRS += $(shell brew --prefix)/include
# LIBRARY_DIRS += $(shell brew --prefix)/lib

# Uncomment to use `pkg-config` to specify OpenCV library paths.
# (Usually not necessary -- OpenCV libraries are normally installed in one of the above $LIBRARY_DIRS.)
# USE_PKG_CONFIG := 1

# N.B. both build and distribute dirs are cleared on `make clean`
BUILD_DIR := build
DISTRIBUTE_DIR := distribute

# Uncomment for debugging. Does not work on OSX due to https://github.com/BVLC/caffe/issues/171
# DEBUG := 1

# The ID of the GPU that 'make runtest' will use to run unit tests.
# "所用的GPU的ID编号"
TEST_GPUID := 0

# enable pretty build (comment to see full commands)
# "默认不打印后面的内容，将这里注释掉，就可以打印出所有内容。"
Q ?= @
~~~

#### makefile 文件配置详解
~~~
sudo gedit Makefile
将
NVCCFLAGS += -ccbin=$(CXX) -Xcompiler-fPIC $(COMMON_FLAGS)
替换为：
NVCCFLAGS += -D_FORCE_INLINES -ccbin=$(CXX) -Xcompiler -fPIC $(COMMON_FLAGS)
将
LIBRARIES += glog gflags protobuf boost_system boost_filesystem m hdf5_hl hdf5
修改为：
LIBRARIES += glog gflags protobuf boost_system boost_filesystem m hdf5_serial_hl hdf5_serial
~~~
