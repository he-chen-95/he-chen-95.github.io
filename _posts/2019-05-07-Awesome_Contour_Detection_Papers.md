---
layout:     post
title:      Awesome Contour Detection Papers
subtitle:   A collection of papers on contour detection
date:       2019-05-07
author:     HE Chen
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - 技术
---

# Awesome Contour Detection Papers

##### 2019-05-07 - Up to date 

A collection of contour and edge detection papers (*a.k.a.* contour detection or boundary detection).

> Feel free to create a PR or an issue.

![examples](https://github.com/he-chen-95/Chen-Image-Host/raw/master/2019/contour-edge-detection.png)

|1st column|2nd column|3 column|
|:---:|:---:|:---:|
|Input Image|general edge detection|object contour detection|

###### Edge detection: 
- **Edges** are abrupt pixels at which the luminance, color or stereo change sharply. So the term 'edge' is mostly used to denote image points where intensity difference between pixels are significant. Pixel-level technique.

- **Edge detection** mainly focuses on the changes in brightness, color, and texture, and aims to extract visually salient edges form natural image. it is usually considered as a low-level technique.

###### Contour detection: 
- **Contours** (or boundaries) are referred to the boundary pixels of meaningful objects. the term 'contour' is used to denote object boundary. Object-level.

- **Contour detection** does edge detection and organizes related edge together to detect border of objects (object-level contours) in images. Thus, in many cases contour detection is performed  by processing the detected edges further.

###### Remarks: 
- These two terms are often used interchangeably.


**Outline**

- [Deep-learning based approaches](#1-deep-learning-based-approaches)
  - [General edge detection](#11-general-edge-detection)
  - [Object contour detection](#12-object-contour-detection)
  - [Semantic edge detection (Category-Aware)](#13-semantic-edge-detection-category-aware)
  - [Occlusion boundary detection](#14-occlusion-boundary-detection)
  - [Edge detection from multi-frames](#15-edge-detection-from-multi-frames)
- [Traditional approaches](#2-traditional-approaches)


## 1. Deep-learning based approaches

### 1.1 General edge detection

| Short name | Paper | Source | Code/Project Link  |
| :---: | :---: | :---: | :---: |
| BDCN | [Bi-Directional Cascade Network for Perceptual Edge Detection](https://arxiv.org/pdf/1902.10903.pdf) | CVPR 2019 | [[code]](https://github.com/pkuCactus/BDCN) |
| LPCB | [Learning to Predict Crisp Boundaries](http://openaccess.thecvf.com/content_ECCV_2018/papers/Ruoxi_Deng_Learning_to_Predict_ECCV_2018_paper.pdf) | ECCV 2018 | - |
| AMH-Net | [Learning Deep Structured Multi-Scale Features using Attention-Gated CRFs for Contour Prediction](https://papers.nips.cc/paper/6985-learning-deep-structured-multi-scale-features-using-attention-gated-crfs-for-contour-prediction.pdf) | NIPS 2017 | [[code]](https://github.com/danxuhk/AttentionGatedMulti-ScaleFeatureLearning) |
| RCF | [Richer Convolutional Features for Edge Detection](http://openaccess.thecvf.com/content_cvpr_2017/papers/Liu_Richer_Convolutional_Features_CVPR_2017_paper.pdf) | CVPR 2017 | [[code-caffe]](https://github.com/yun-liu/rcf) [[code-pytorch]](https://github.com/meteorshowers/RCF-pytorch) [[project]](https://mmcheng.net/zh/rcfEdge/) |
| CED | [Deep Crisp Boundaries](http://openaccess.thecvf.com/content_cvpr_2017/papers/Wang_Deep_Crisp_Boundaries_CVPR_2017_paper.pdf) | CVPR 2017 | [[code]](https://github.com/Wangyupei/CED) |
| RDS | [Learning Relaxed Deep Supervision for Better Edge Detection](http://openaccess.thecvf.com/content_cvpr_2016/papers/Liu_Learning_Relaxed_Deep_CVPR_2016_paper.pdf) | CVPR 2016 | - |
| HFL | [High-for-Low and Low-for-High: Efficient Boundary Detection from Deep Object Features and its Applications to High-Level Vision](http://openaccess.thecvf.com/content_iccv_2015/papers/Bertasius_High-for-Low_and_Low-for-High_ICCV_2015_paper.pdf) | ICCV 2015 | [[code]](https://github.com/gberta/HFL_code) |
| HED | [Holistically-Nested Edge Detection](http://openaccess.thecvf.com/content_iccv_2015/papers/Xie_Holistically-Nested_Edge_Detection_ICCV_2015_paper.pdf) | ICCV 2015 | [[code]](https://github.com/s9xie/hed) |
| Pixel-wise | [Pixel-wise Deep Learning for Contour Detection](https://arxiv.org/pdf/1504.01989.pdf) | ICLR 2015 | - |
| DeepEdge | [DeepEdge: A Multi-Scale Bifurcated Deep Network for Top-Down Contour Detection](http://openaccess.thecvf.com/content_cvpr_2015/papers/Bertasius_DeepEdge_A_Multi-Scale_2015_CVPR_paper.pdf) | CVPR 2015 | - |
| DeepContour | [DeepContour: A Deep Convolutional Feature Learned by Positive-sharing Loss for Contour Detection](http://openaccess.thecvf.com/content_cvpr_2015/papers/Shen_DeepContour_A_Deep_2015_CVPR_paper.pdf) | CVPR 2015 | [[code]](https://github.com/shenwei1231/DeepContour) |
| N4-Field |[N4-fields: Neural network nearest neighbor fields for image transforms](https://arxiv.org/abs/1406.6558)| arXiv 2014 | - |
| DeepNet | [Visual Boundary Prediction: A Deep Neural Prediction Network and Quality Dissection](http://homepages.inf.ed.ac.uk/ckiw/postscript/aistats14.pdf) | AIStats 2014 | - |

### 1.2 Object contour detection

| Short name | Paper | Source | Code/Project Link  |
| :---: | :---: | :---: | :---: |
| RefineContourNet | [Object Contour and Edge Detection with RefineContourNet](https://arxiv.org/abs/1904.13353) | arXiv 2019 | - |
| contouGAN | [Image contour detection with generative adversarial network](https://www.sciencedirect.com/science/article/abs/pii/S0950705118304842) | Elsevier 2018 | [[code]](https://github.com/sxdxedu/ContourGAN) |
| COB | [Convolutional Oriented Boundaries](https://arxiv.org/pdf/1608.02755.pdf) | ECCV 2016 | [[code]](https://github.com/kmaninis/COB) [[project]](http://www.vision.ee.ethz.ch/~cvlsegmentation/cob/index.html) |
| CEDN | [Object Contour Detection with a Fully Convolutional Encoder-Decoder Network](http://openaccess.thecvf.com/content_cvpr_2016/papers/Yang_Object_Contour_Detection_CVPR_2016_paper.pdf) | CVPR 2016 | [[code-caffe]](https://github.com/jimeiyang/objectContourDetector) [[code-TF]](https://github.com/Raj-08/tensorflow-object-contour-detection) |
| - | [Weakly Supervised Object Boundaries](http://openaccess.thecvf.com/content_cvpr_2016/papers/Khoreva_Weakly_Supervised_Object_CVPR_2016_paper.pdf) | CVPR 2016 | - |


### 1.3 Semantic edge detection (Category-Aware)

| Short name | Paper | Source | Code/Project Link  |
| :---: | :---: | :---: | :---: |
| STEAL | [Devil is in the Edges: Learning Semantic Boundaries from Noisy Annotations](https://arxiv.org/pdf/1904.07934.pdf) | CVPR 2019 | [[project]](https://nv-tlabs.github.io/STEAL/) |
| DFF | [Dynamic Feature Fusion for Semantic Edge Detection](https://arxiv.org/pdf/1902.09104.pdf) | 1902.09104 | - |
| SEAL | [Simultaneous Edge Alignment and Learning](http://openaccess.thecvf.com/content_ECCV_2018/papers/Zhiding_Yu_SEAL_A_Framework_ECCV_2018_paper.pdf) | ECCV 2018 | [[code]](https://github.com/Chrisding/seal) |
| CASENet | [CASENet: Deep Category-Aware Semantic Edge Detection](http://openaccess.thecvf.com/content_cvpr_2017/papers/Yu_CASENet_Deep_Category-Aware_CVPR_2017_paper.pdf) | CVPR 2017 | [[code]](http://www.merl.com/research/license#CASENet) |
| `dataset` | [Semantic Contours from Inverse Detectors](https://www.robots.ox.ac.uk/~vgg/rg/papers/BharathICCV2011.pdf) | ICCV 2011 | [[code]](https://github.com/bharath272/semantic_contours) |


### 1.4 Occlusion boundary detection

| Short name | Paper | Source | Code/Project Link  |
| :---: | :---: | :---: | :---: |
| - | [Occlusion Boundary Detection via Deep Exploration of Context](http://openaccess.thecvf.com/content_cvpr_2016/papers/Fu_Occlusion_Boundary_Detection_CVPR_2016_paper.pdf) | CVPR 2016 | - |


### 1.5 Edge detection from multi-frames

| Short name | Paper | Source | Code/Project Link  |
| :---: | :---: | :---: | :---: |
| Boundary Flow | [Boundary Flow: A Siamese Network that Predicts Boundary Motion without Training on Motion](http://openaccess.thecvf.com/content_cvpr_2018/papers/Lei_Boundary_Flow_A_CVPR_2018_paper.pdf) | CVPR 2018 | - |
| LEGO | [LEGO: Learning Edge with Geometry all at Once by Watching Videos](http://openaccess.thecvf.com/content_cvpr_2018/papers/Yang_LEGO_Learning_Edge_CVPR_2018_paper.pdf) | CVPR 2018 | [[code]](https://github.com/zhenheny/LEGO) |
| - | [Unsupervised Learning of Edges](http://openaccess.thecvf.com/content_cvpr_2016/papers/Li_Unsupervised_Learning_of_CVPR_2016_paper.pdf) | CVPR 2016 | [[code]](https://github.com/happyharrycn/unsupervised_edges) |


---


## 2. Traditional approaches

| Short name | Paper | Source | Code/Project Link  |
| :---: | :---: | :---: | :---: |
| SemiContour | [SemiContour: A Semi-supervised Learning Approach for Contour Detection](http://openaccess.thecvf.com/content_cvpr_2016/papers/Zhang_SemiContour_A_Semi-Supervised_CVPR_2016_paper.pdf) | CVPR 2016 | - |
| OEF | [Oriented Edge Forests for Boundary Detection](http://openaccess.thecvf.com/content_cvpr_2015/papers/Hallman_Oriented_Edge_Forests_2015_CVPR_paper.pdf) |  CVPR 2015 | [[code]](https://github.com/samhallman/oef) |
| SE | [Fast edge detection using structured forests](https://arxiv.org/pdf/1406.5549.pdf) | TPAMI 2015 | [[code]](https://github.com/pdollar/edges) |
| Edge Boxes | [Edge Boxes: Locating Object Proposals from Edges](https://www.microsoft.com/en-us/research/wp-content/uploads/2014/09/ZitnickDollarECCV14edgeBoxes.pdf) | ECCV 2014 | [[code]](https://github.com/pdollar/edges) |
| PMI | [Crisp Boundary Detection Using Pointwise Mutual Information](https://link.springer.com/chapter/10.1007/978-3-319-10578-9_52) | ECCV 2014 | [[code]](https://github.com/phillipi/crisp-boundaries) |
| Sketch Tokens | [Sketch tokens: A learned mid-level representation for contour and object detection](http://openaccess.thecvf.com/content_cvpr_2013/papers/Lim_Sketch_Tokens_A_2013_CVPR_paper.pdf) | CVPR 2013 | - |
| SCG | [Discriminatively Trained Sparse Code Gradients for Contour Detection](http://papers.nips.cc/paper/4787-discriminatively-trained-sparse-code-gradients-for-contour-detection.pdf) | NIPS 2012 | - |
| gPb-owt-ucm | [Contour Detection and Hierarchical Image Segmentation](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.374.3367&rep=rep1&type=pdf) | TPAMI 2011 | [[code]](http://www.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/BSR/BSR_source.tgz) [[project]](https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/resources.html) |
| Multi-scale |[Multi-scale Improves Boundary Detection in Natural Images](https://homes.cs.washington.edu/~xren/publication/xren_eccv08_multipb.pdf)| 2008 ECCV | - |
| BEL | [Supervised Learning of Edges and Object Boundaries](https://ieeexplore.ieee.org/abstract/document/1640993)| IEEE 2006 | - |
| Pb | [Learning to Detect Natural Image BoundariesUsing Local Brightness, Color,and Texture Cues](https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/papers/mfm-pami-boundary.pdf)| IEEE Transactions 2004 | - |
| Statistical Edge | [Learning and Evaluating Edge Cues](https://pdfs.semanticscholar.org/c941/cda0e9af033628fb1de85f02e3cedd4d57e0.pdf)| IEEE Transactions 2003 | - |
| Canny | [A Computational Approach to Edge Detection](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.420.3300&rep=rep1&type=pdf) | TPAMI 1986 | - |
| Zero-crossing | [On Edge Detection](https://ieeexplore.ieee.org/document/4767769) | IEEE Transactions 1986 | - |
| Sobel | [On the accuracy of the Sobel edge detector](https://www.sciencedirect.com/science/article/pii/0262885683900069)| 1983 Elsevier | - |
