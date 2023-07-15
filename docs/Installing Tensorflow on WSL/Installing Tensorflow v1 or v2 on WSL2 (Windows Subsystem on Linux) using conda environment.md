# Introduction
GPU support on native-Windows is only available for 2.10 or earlier versions, starting in TF 2.11, CUDA build is not supported for Windows. For using TensorFlow GPU on Windows, you will need to build/install TensorFlow in WSL2 
https://www.tensorflow.org/install/source_windows#gpu

Conda installation guide: [Installing on Linux](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html), please run this command in WSL.

## For v2.x

For finding compatible CUDA and cuDNN versions for each Tensorflow [Build from source  |  TensorFlow](https://www.tensorflow.org/install/source)
___BUILD IN PROGRESS___

## For v1.x
With the release of TF 2.0, Google announced that new major releases will not be provided on the TF 1.x branch after the release of TF 1.15 on October 14. And older version of Tensorflow will need different version of CUDA and cuDNN. And also even you are able to find the older version of CUDA and cuDNN version on NVIDIA archives. RTX 30xx cards requires CUDA 10 and above.

So in order to install TF v1, you can use a modified version of tensorflow from NVIDIA from [HERE](https://github.com/NVIDIA/tensorflow) which makes it backward compatible for RTX 30xx cards and also for other GPU cards and this modified version of Tensorflow can also use the latest version of cuDNN.

### Requirements
- Ubuntu 20.04 or later (64-bit)
- GPU support requires a CUDA®-enabled card
- For NVIDIA GPUs, the r455 driver must be installed
__For wheel installation__:
- Python 3.8
- pip 20.3 or later

### Install

````
$ pip install --user nvidia-pyindex
$ pip install --user nvidia-tensorflow[horovod]
````
The `nvidia-tensorflow` package includes CPU and GPU support for Linux. After that, you need to install `cuda-toolkit` and `nvidia-cudnn`.
``````bash
conda install -c conda-forge cudatoolkit=11.8.0
python3 -m pip install nvidia-cudnn-cu11==8.6.0.163
mkdir -p $CONDA_PREFIX/etc/conda/activate.d

echo 'CUDNN_PATH=$(dirname $(python -c "import nvidia.cudnn;print(nvidia.cudnn.__file__)"))' >> $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh

echo 'export LD_LIBRARY_PATH=$CONDA_PREFIX/lib/:$CUDNN_PATH/lib:$LD_LIBRARY_PATH' >> $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh

source $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh

# Verify install:
python3 -c "import tensorflow as tf; tf.test.is_gpu_available()"

``````
For newer CUDA versions and updated instructions. [Install TensorFlow with pip](https://www.tensorflow.org/install/pip)
If `CUDA` and `cuDNN` is correctly installed, then you can see in the last line of my GPU (RTX 3050 Laptop GPU). ![[Screenshot 2023-07-16 000737.png]]

