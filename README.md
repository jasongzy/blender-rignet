# bRigNet

Neural Rigging for [blender](https://www.blender.org/ "Blender Home Page") using [RigNet](https://zhan-xu.github.io/rig-net/ "RigNet Home Page")

## Table of Contents

1. [Introduction](#introduction)
2. [Setup](#setup)
3. [Installation](#installation)
   - [Install dependencies via "Install" button](#install-dependencies-via-install-button)
   - [Install dependencies using _conda_](#install-dependencies-using-conda)
   - [Install dependencies using virtualenv](#install-dependencies-using-virtualenv)
4. [Usage](#usage)
5. [Training](#training)
6. [Disclaimer](#disclaimer)
7. [License](#license)

## Introduction <a name="introduction"></a>

Blender is the open source 3D application from the Blender Foundation. RigNet is the Machine Learning prediction
for articulated characters.

## Setup <a name="setup"></a>

bRigNet requires SciPy, PyTorch and torch-geometric, along with torch-scatter and torch-sparse.

## Installation <a name="installation"></a>

Download the Neural Rigging add-on as a .zip file and install it from the blender addons window,
or copy the code to the blender scripts path

### Install dependencies via "Install" button <a name="install-dependencies-via-install-button"></a>

At present, the CUDA toolkit from nVidia is required, it can be found at the
[manufacturer website](https://developer.nvidia.com)

A dependency installer is available in the preferences.

- Install CUDA. At present prebuilt packages support versions 10.1, 10.2, 11.1
- In the addon preferences, make sure that the Cuda version is detected correctly.
- Hit the "Install" button. It can take time!

Alternatively, Environment managers, like conda or virtualenv can be used to ease the install.

### Install dependencies using _conda_ <a name="install-dependencies-using-conda"></a>

Anaconda is a data science platform from Anaconda Inc., it can be downloaded from the
[company website](https://www.anaconda.com/).

A lightweight version called [Miniconda](https://docs.conda.io/en/latest/miniconda.html) is available.
Both versions include the package manager 'conda' used in the following steps.

- Open a Miniconda or Anaconda prompt
- Create a Conda Environment and activate it

```bash
conda create -n brignet python=3.7
conda activate brignet_deps
```

- Install PyTorch. If CUDA is installed, the CUDA version can be queried in a command prompt. For example

```bash
nvcc --version
```

```bash
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2019 NVIDIA Corporation
Built on Wed_Oct_23_19:32:27_Pacific_Daylight_Time_2019
Cuda compilation tools, release 10.2, V10.2.89
```

In this case PyTorch can be installed in the command prompt via

```bash
conda install pytorch==1.8.1 cudatoolkit=10.2 -c pytorch
```

More complete information on the PyTorch command line can be found at the [PyTorch website](https://pytorch.org/)
The install command on non-cuda devices is

```bash
conda install pytorch==1.8.1 cpuonly -c pytorch
```

- Install torch utilities. The syntax follows the pattern

```bash
pip install [package-name] -f https://pytorch-geometric.com/whl/torch-[version]+cu[cuda-version].html
```

```bash
pip install torch-scatter -f https://pytorch-geometric.com/whl/torch-1.8.1+cu102.html
pip install torch-sparse -f https://pytorch-geometric.com/whl/torch-1.8.1+cu102.html
pip install torch-cluster -f https://pytorch-geometric.com/whl/torch-1.8.1+cu102.html
pip install torch-spline-conv -f https://pytorch-geometric.com/whl/torch-1.8.1+cu102.html
pip install torch-geometric
```

Alternatively, pip can try and build the libraries. Even if part of torch-sparse fails without a proper environment,
the relevant modules are usually built

```bash
pip install torch-scatter
pip install torch-sparse
pip install torch-geometric
```

The directory of each environment can be obtained via

```bash
conda info --envs
```

The environment directory can be set in the "Additional Modules" setting of the bRigNet preferences

### Install dependencies using virtualenv <a name="install-dependencies-using-virtualenv"></a>

virtualenv can be used to create a Python environment with the required packages.
First, python 3.7 must be installed on the system. It can be found at https://www.python.org/downloads/

Make sure that **Add Python 3.7 to PATH** is checked in the setup options.

Usually, python comes with its package manager installed (pip). Please, refer
to the [pip documentation](https://pypi.org/project/pip/) if pip is not present in your system.

Next step is to install virtualenv. Open a command prompt and reach a folder where python packages will be kept
please execute.

```bash
pip install virtualenv
```

then create the virtual environment and activate it

```bash
virtualenv brignet_deps
cd brignet_deps
Scripts\activate
```

now we can install the torch library. At present, version 1.8.1 is provided.
torch-geometric provides prebuilt packages for CUDA 10.1, 10.2, 11.1

CUDA 10.2 is used in this example:

```bash
pip install torch==1.8.1+cu102 -f https://download.pytorch.org/whl/torch_stable.html
pip install torch-scatter -f https://pytorch-geometric.com/whl/torch-1.8.1+cu102.html
pip install torch-sparse -f https://pytorch-geometric.com/whl/torch-1.8.1+cu102.html
pip install torch-cluster -f https://pytorch-geometric.com/whl/torch-1.8.1+cu102.html
pip install torch-spline-conv -f https://pytorch-geometric.com/whl/torch-1.8.1+cu102.html
pip install torch-geometric
```

the virtual environment directory can be set as the "Additional modules path" in the brignet preferences

## Usage <a name="usage"></a>

Enable _bRigNet_ in the blender addons, the preferences will show up.
Set the Modules path properties to the RigNet environment from the previous step

RigNet requires a trained model. They have made theirs available at [this address](https://umass-my.sharepoint.com/:u:/g/personal/zhanxu_umass_edu/EYKLCvYTWFJArehlo3-H2SgBABnY08B4k5Q14K7H1Hh0VA)
The checkpoint folder can be copied to the RigNet subfolder.
A different location can be set in the addon preferences.

#### Rig Generation

the **bRigNet** tab will show up in the Viewport tools. Select a character mesh as target.
Please make sure it doesn't exceed the 5K triangles. You can use the _Decimator_ modifier
to reduce the polycount on a copy of the mesh, and select a _Collection_ of high res model
on which to transfer the final weights

#### Load generated rigs

Rigs generated using RigNet from the command line can be loaded via the **Load Skeleton** panel.
Please select the _.obj and _.txt file and press the button **Load Rignet character**

## Training <a name="training"></a>

The blender addon doesn't cover training yet. If you want to train your own model, please follow the instructions
from the [RigNet project](https://github.com/zhan-xu/RigNet#training).

## License <a name="license"></a>

This addon is released under the GNU General Public License version 3 (GPLv3).
The RigNet subfolder is licensed under the General Public License Version 3 (GPLv3), or under a Commercial License.
