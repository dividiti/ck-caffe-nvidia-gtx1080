# [cknowledge.org/ai](http://cknowledge.org): Crowdsourcing benchmarking and optimisation of AI

## [PUBLIC] Benchmarking Caffe on NVIDIA GTX 1080

**NB:** The Caffe experimental results are released with approval from General Motors.

The Jupyter notebook ([view on github.com](https://github.com/dividiti/ck-caffe-nvidia-gtx1080/blob/master/script/analysis/ck-caffe-nvidia-gtx1080.20170518.ipynb); [view on nbviewer.jupyter.org](https://nbviewer.jupyter.org/github/dividiti/ck-caffe-nvidia-gtx1080/blob/master/script/analysis/ck-caffe-nvidia-gtx1080.20170518.ipynb?raw)) in this Collective Knowledge repository analyses the performance (execution time, memory consumption):
- on **[dividiti](http://dividiti.com)**'s **velociti** Hewlett-Packard Z640 Workstation ([G1X62EA](http://h20195.www2.hp.com/v2/default.aspx?cc=ie&lc=en&oid=7528701)):
  - [Intel(R) Xeon(R) CPU E5-2650 v3](http://ark.intel.com/products/81705/Intel-Xeon-Processor-E5-2650-v3-25M-Cache-2_30-GHz):
    - 10 cores, 20 threads;
    - Base clock 2300 MHz, turbo clock 3000 MHz;
    - Max power consumption 105 Watt;
    - Max memory bandwidth 68 GB/s;
    - RAM memory 32 GB DDR4;
```
$ uname -a
Linux velociti 4.4.0-45-generic #66-Ubuntu SMP Wed Oct 19 14:12:37 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
$ cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.04
DISTRIB_CODENAME=xenial
DISTRIB_DESCRIPTION="Ubuntu 16.04.1 LTS"
```
  - [NVIDIA GeForce GTX 1080 "Founders Edition"](http://www.geforce.co.uk/hardware/10series/geforce-gtx-1080/):
    - Pascal architecture;
    - 2560 CUDA cores;
    - Base clock 1607 MHz, boost clock 1733 MHz;
    - Max power consumption 180 Watt;
    - RAM memory 8 GB GDDR5X;
    - Max memory bandwidth 320 GB/s;
    - GPU Driver 367.57 [10/Oct/2016];
    - CUDA Toolkit 8.0.44 [xx/Sep/2016].

- using 14 Caffe **libraries**:
  - [`tag`] **Branch** (**revision hash, date**): **math libraries**.
  - [`cpu`] Master ([4ba654f](https://github.com/BVLC/caffe/commit/4ba654f5c88c36ee8ba53964b7faf25c6d7010b4), 5/Oct/2016): with [OpenBLAS 0.2.19](https://github.com/xianyi/OpenBLAS/releases/tag/v0.2.19);
  - [`cuda`] Master ([4ba654f](https://github.com/BVLC/caffe/commit/4ba654f5c88c36ee8ba53964b7faf25c6d7010b4), 5/Oct/2016): with [cuBLAS](https://developer.nvidia.com/cublas) (part of CUDA Toolkit 8.0.44);
  - [`cudnn`] Master ([4ba654f](https://github.com/BVLC/caffe/commit/4ba654f5c88c36ee8ba53964b7faf25c6d7010b4), 5/Oct/2016): with [cuDNN 5.1](https://developer.nvidia.com/cudnn);
  - [`nvidia-cuda`] NVIDIA v0.15 ([1024d34](https://github.com/NVIDIA/caffe/commit/1024d34d93cd34a9013d6fac4e56e45162073d38), 17/Nov/2016): with [cuBLAS](https://developer.nvidia.com/cublas) (part of CUDA Toolkit 8.0.44);
  - [`nvidia-cudnn`] NVIDIA v0.15 ([1024d34](https://github.com/NVIDIA/caffe/commit/1024d34d93cd34a9013d6fac4e56e45162073d38), 17/Nov/2016): with [cuDNN 5.1](https://developer.nvidia.com/cudnn);
  - [`nvidia-fp16-cuda`] NVIDIA experimental/fp16 ([fca1cf4](https://github.com/NVIDIA/caffe/commit/fca1cf475d1d0a6d355f8b9877abcc4e13951c9c), 11/Jul/2016): with [cuBLAS](https://developer.nvidia.com/cublas) (part of CUDA Toolkit 8.0.44);
  - [`nvidia-fp16-cudnn`] NVIDIA experimental/fp16 ([fca1cf4](https://github.com/NVIDIA/caffe/commit/fca1cf475d1d0a6d355f8b9877abcc4e13951c9c), 11/Jul/2016): with [cuDNN 5.1](https://developer.nvidia.com/cudnn);
  - [`clblas`] OpenCL ([9abafdc](https://github.com/BVLC/caffe/commit/9abafdca7b91ff5cd6f29035fdc882c269409f27), 7/Oct/2016): with [ViennaCL 1.7.1](https://github.com/viennacl/viennacl-dev/releases/tag/release-1.7.1) and [clBLAS 2.10](https://github.com/clMathLibraries/clBLAS/releases/tag/v2.10);
  - [`clblast`] OpenCL ([9abafdc](https://github.com/BVLC/caffe/commit/9abafdca7b91ff5cd6f29035fdc882c269409f27), 7/Oct/2016): with [ViennaCL 1.7.1](https://github.com/viennacl/viennacl-dev/releases/tag/release-1.7.1) and [CLBlast 0.9.0](https://github.com/CNugteren/CLBlast/releases/tag/0.9.0);
  - [`viennacl`] OpenCL ([9abafdc](https://github.com/BVLC/caffe/commit/9abafdca7b91ff5cd6f29035fdc882c269409f27), 7/Oct/2016): with [ViennaCL 1.7.1](https://github.com/viennacl/viennacl-dev/releases/tag/release-1.7.1) only;
  - [`libdnn-cuda`] OpenCL ([cfaaae1](https://github.com/BVLC/caffe/commit/cfaaae1e8c95cc742d045dab2099c8404e726686), 25/Oct/2016): with [libDNN](https://github.com/BVLC/caffe/issues/4155) and [cuBLAS](https://developer.nvidia.com/cublas);
  - [`libdnn-clblas`] OpenCL ([cfaaae1](https://github.com/BVLC/caffe/commit/cfaaae1e8c95cc742d045dab2099c8404e726686), 25/Oct/2016): with [libDNN](https://github.com/BVLC/caffe/issues/4155), [ViennaCL 1.7.1](https://github.com/viennacl/viennacl-dev/releases/tag/release-1.7.1) and [clBLAS 2.10](https://github.com/clMathLibraries/clBLAS/releases/tag/v2.10);
  - [`libdnn-clblast`] OpenCL ([cfaaae1](https://github.com/BVLC/caffe/commit/cfaaae1e8c95cc742d045dab2099c8404e726686), 25/Oct/2016): with [libDNN](https://github.com/BVLC/caffe/issues/4155), [ViennaCL 1.7.1](https://github.com/viennacl/viennacl-dev/releases/tag/release-1.7.1) and [CLBlast 0.9.0](https://github.com/CNugteren/CLBlast/releases/tag/0.9.0);
  - [`libdnn-viennacl`] OpenCL ([cfaaae1](https://github.com/BVLC/caffe/commit/cfaaae1e8c95cc742d045dab2099c8404e726686), 25/Oct/2016): with [libDNN](https://github.com/BVLC/caffe/issues/4155) and [ViennaCL 1.7.1](https://github.com/viennacl/viennacl-dev/releases/tag/release-1.7.1).
  
- using 4 CNN **models**:
  - [GoogleNet](https://github.com/BVLC/caffe/tree/master/models/bvlc_googlenet);
  - [AlexNet](https://github.com/BVLC/caffe/tree/master/models/bvlc_alexnet);
  - [SqueezeNet 1.0](https://github.com/DeepScale/SqueezeNet/tree/master/SqueezeNet_v1.0);
  - [SqueezeNet 1.1](https://github.com/DeepScale/SqueezeNet/tree/master/SqueezeNet_v1.1);

- with the **batch size** varying from 2 to 16 with step 2.
