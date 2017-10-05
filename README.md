# Bonseyes Official Caffe 1.0 Version
###### Caffe-jacinto

Bonseyes Caffe-jacinto is a fork of [tidsp/caffe-jacinto](https://github.com/tidsp/caffe-jacinto) which is a fork of [NVIDIA/caffe](https://github.com/NVIDIA/caffe), which in-turn is derived from [BVLC/Caffe](https://github.com/BVLC/caffe). The modifications in this fork enable training of sparse, quantized CNN models - resulting in low complexity models that can be used in embedded platforms.

The following additional caffe layers have been integrated:

- Single shot detection (SDD) (https://github.com/weiliu89/caffe/tree/ssd)
- Sphereface (https://github.com/wy1iu/sphereface)
- Squeeze and excitation networks (https://github.com/hujie-frank/SENet)

Modifications relative to [BVLC/Caffe]:

- Pooling layer have been modified from ceil to floor to be compatible to pytorch

### Installation
* After cloning the source code, switch to the branch caffe-0.16, if it is not checked out already.
-- *git checkout caffe-0.16*

* Please see the [installation instructions](INSTALL.md) for installing the dependencies and building the code. 

### Additional Information (can be skipped)

New layers and options have been added to support sparsity and quantization. A brief explanation is given in this section, but more details can be found by [clicking here](FEATURES.md). 

Note that Caffe-jacinto does not directly support any embedded/low-power device. But the models trained by it can be used for fast inference on such a device due to the sparsity and quantization.

###### Additional layers
* ImageLabelData and IOUAccuracy layers have been added to train for semantic segmentation.

###### Sparsity
* Measuring sparsity in convolution layers while training is in progress. 
* Thresholding tool to zero-out some convolution weights in each layer to attain certain sparsity in each layer.
* Sparse training methods: zeroing out of small coefficients during training, or fine tuning without updating the zero coefficients - similar to caffe-scnn [paper](https://arxiv.org/abs/1608.03665), [code](https://github.com/wenwei202/caffe/tree/scnn)

###### Quantization
* Collecting statistics (range of weights) to enable quantization
* Dynamic -8 bit fixed point quantization, improved from Ristretto [paper](https://arxiv.org/abs/1605.06402), [code](https://github.com/pmgysel/caffe)

###### Absorbing Batch Normalization into convolution weights
* A tool is provided to absorb batch norm values into convolution weights. This may help to speedup inference. This will also help if Batch Norm layers are not supported in an embedded implementation.

<br>
The following sections are kept as it is from the original Caffe.

# Caffe

Caffe is a deep learning framework made with expression, speed, and modularity in mind.
It is developed by the Berkeley Vision and Learning Center ([BVLC](http://bvlc.eecs.berkeley.edu))
and community contributors.

# NVCaffe

NVIDIA Caffe ([NVIDIA Corporation &copy;2017](http://nvidia.com)) is an NVIDIA-maintained fork
of BVLC Caffe tuned for NVIDIA GPUs, particularly in multi-GPU configurations.
Here are the major features:
* **16 bit (half) floating point train and inference support**.
* **Mixed-precision support**. It allows to store and/or compute data in either 
64, 32 or 16 bit formats. Precision can be defined for every layer (forward and 
backward passes might be different too), or it can be set for the whole Net.
* **Integration with  [cuDNN](https://developer.nvidia.com/cudnn) v6**.
* **Automatic selection of the best cuDNN convolution algorithm**.
* **Integration with v1.3.4 of [NCCL library](https://github.com/NVIDIA/nccl)**
 for improved multi-GPU scaling.
* **Optimized GPU memory management** for data and parameters storage, I/O buffers 
and workspace for convolutional layers.
* **Parallel data parser and transformer** for improved I/O performance.
* **Parallel back propagation and gradient reduction** on multi-GPU systems.
* **Fast solvers implementation with fused CUDA kernels for weights and history update**.
* **Multi-GPU test phase** for even memory load across multiple GPUs.
* **Backward compatibility with BVLC Caffe and NVCaffe 0.15**.
* **Extended set of optimized models** (including 16 bit floating point examples).


## License and Citation

Caffe is released under the [BSD 2-Clause license](https://github.com/BVLC/caffe/blob/master/LICENSE).
The BVLC reference models are released for unrestricted use.

Please cite Caffe in your publications if it helps your research:

    @article{jia2014caffe,
      Author = {Jia, Yangqing and Shelhamer, Evan and Donahue, Jeff and Karayev, Sergey and Long, Jonathan and Girshick, Ross and Guadarrama, Sergio and Darrell, Trevor},
      Journal = {arXiv preprint arXiv:1408.5093},
      Title = {Caffe: Convolutional Architecture for Fast Feature Embedding},
      Year = {2014}
    }
