# Nebullvm

This repository contains the opensource `nebullvm` package, an opensource project
aiming to reunite all the opensource AI compiler under the same easy-to-use interface.

## Installation
There are two ways of installing `nebullvm`. Using PyPy or from the source code.
For using the stable version we suggest installing the library with `pip`, for 
getting the newest features install the library from the source code.

### Source code installation
For installing the source code you must clone the directory on your local machine
using `git`
```
git clone https://github.com/nebuly-ai/nebullvm.git
```
Then, enter into the repo and install with `pip`
```
cd nebullvm
pip install .
```
### Installation with PyPy
The easiest way for installing `nebullvm` is using `pip`, running
```
pip install nebullvm
```
### Possible issues
**MacOS**: the installation may fail on MacOS for MacBooks with the Apple Silicon chip,
due to compilation errors of scipy. The easy fix is to install scipy with another
package manager as conda (the Apple Silicon distribution of Mini-conda) and then install
`nebullvm`.
For any additional problem do not hesitate to open an issue or to contact directly
`info@nebuly.ai` by email.

## Get Started
The `nebullvm` aims at reducing by at least 5x computation time due to 
deep learning models inference, using the right compiler on specific machines.
At the current state `nebullvm` supports model optimization from the `torch` 
and `tensorflow` frameworks, but others will be added soon. 
Models can easily be imported from one of the supported framework 
using the apposite function.
Here, we present an example for optimizing a pytorch model:
```
>>> import torch
>>> import torchvision.models as models
>>> from nebullvm import optimize_torch_model
>>> model = models.efficientnet_b0()
>>> bs, input_sizes = 1, [(3, 256, 256)]
>>> save_dir = "."
>>> optimized_model = optimize_torch_model(
...     model, batch_size=bs, input_sizes=input_sizes, save_dir=save_dir
... )
>>> x = torch.randn((bs, *input_sizes[0]))
>>> res = optimized_model(x)
```
A similar example can be done with `tensorflow` using the function 
`nebullvm.optimize_tf_model`.

The library automatically installs the compilers available for a particular 
hardware. However, if you prefer avoiding this behaviour, you can simply 
export the environmental variable `NO_COMPILER_INSTALLATION=1`, running
```
export NO_COMPILER_INSTALLATION=1
```
from your command line or adding
```
import os
os.environ["NO_COMPILER_INSTALLATION"] = "1"
```
in your python code before importing `nebullvm` for the first time.

Note that auto-installation of the opensource compilers is done outside nebullvm's wheel. 
The ApacheTVM and Openvino installations have been tested on MacOS, Debian-like and CentOS-like
linux distributions. 

The feature is still in an alpha version, so we expect it may fail under
non-tested circumstances. We are doing our best for supporting the largest number of
hardware configuration, operating systems and development frameworks, thus warmly invite you to
open a new github-issue any time you encounter a bug or a failure of the library.


## Acknowledgments

This library is based on the amazing job made by the opensource community and the
main hardware providers on building AI compilers. The aim of `nebullvm` is to group
the amazing job done so far in a common interface in order to squeeze out the 
performance from developers hardware. At the current state `nebullvm`supports
as AI compilers:
* OpenVino (on Intel Machines)
* Tensor RT (on Nvidia GPUs)
* Apache TVM
