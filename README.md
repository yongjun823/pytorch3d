## Install in NVIDIA RTX 3070
1. Install requirements and Setup CUB
reference : https://github.com/facebookresearch/pytorch3d/blob/master/INSTALL.md <br>
Otherwise download the CUB library from https://github.com/NVIDIA/cub/releases and unpack it to a folder of your choice. Define the environment variable CUB_HOME before building and point it to the directory that contains CMakeLists.txt for CUB. For example on Linux/Mac,
``` sh
curl -LO https://github.com/NVIDIA/cub/archive/1.10.0.tar.gz
tar xzf 1.10.0.tar.gz
export CUB_HOME=$PWD/cub-1.10.0
```
1.1 conda install
```
conda install -yc conda-forge fvcore
conda install -yc iopath iopath
```

2. Set environment variable
``` sh
export TORCH_CUDA_ARCH_LIST="8.0"
```
3. Download source code
``` sh
git clone https://github.com/yongjun823/pytorch3d && cd pytorch3d
```
4. Update setup.py

``` python
    extra_compile_args = {"cxx": ["-std=c++14"],
                          'nvcc':['--gpu-architecture=compute_80','--gpu-code=sm_80']
                           }
```
5. Install pytorch3d
```
pip3 install -e .
```

## Install in NVIDIA docker nvcr.io/nvidia/pytorch:19.12-py3

0. Update pip & apt
```
apt-get update
apt install -y libusb-1.0-0 libgl1-mesa-glx
pip install -U pip
```

1. Create anaconda environment
``` sh
conda create -n pytorch3d python=3.8
conda init bash
source ~/.bashrc 
conda activate pytorch3d
```

2. Install anaconda package (CUDA 10.2 & torch 1.7)
``` sh
conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch
conda install -yc conda-forge fvcore 
conda install -yc iopath iopath
conda install -yc bottler nvidiacub
```

3. set CUB_HOME
``` sh
curl -LO https://github.com/NVIDIA/cub/archive/1.10.0.tar.gz
tar xzf 1.10.0.tar.gz
export CUB_HOME=$PWD/cub-1.10.0
```

4. Install Pytorch3d
``` sh
pip install "git+https://github.com/facebookresearch/pytorch3d.git@stable"
```


<img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/pytorch3dlogo.png" width="900"/>

[![CircleCI](https://circleci.com/gh/facebookresearch/pytorch3d.svg?style=svg)](https://circleci.com/gh/facebookresearch/pytorch3d)
[![Anaconda-Server Badge](https://anaconda.org/pytorch3d/pytorch3d/badges/version.svg)](https://anaconda.org/pytorch3d/pytorch3d)

# Introduction

PyTorch3D provides efficient, reusable components for 3D Computer Vision research with [PyTorch](https://pytorch.org).

Key features include:

- Data structure for storing and manipulating triangle meshes
- Efficient operations on triangle meshes (projective transformations, graph convolution, sampling, loss functions)
- A differentiable mesh renderer

PyTorch3D is designed to integrate smoothly with deep learning methods for predicting and manipulating 3D data.
For this reason, all operators in PyTorch3D:

- Are implemented using PyTorch tensors
- Can handle minibatches of hetereogenous data
- Can be differentiated
- Can utilize GPUs for acceleration

Within FAIR, PyTorch3D has been used to power research projects such as [Mesh R-CNN](https://arxiv.org/abs/1906.02739).

## Installation

For detailed instructions refer to [INSTALL.md](INSTALL.md).

## License

PyTorch3D is released under the [BSD-3-Clause License](LICENSE).

## Tutorials

Get started with PyTorch3D by trying one of the tutorial notebooks.

|<img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/dolphin_deform.gif" width="310"/>|<img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/bundle_adjust.gif" width="310"/>|
|:-----------------------------------------------------------------------------------------------------------:|:--------------------------------------------------:|
| [Deform a sphere mesh to dolphin](https://github.com/facebookresearch/pytorch3d/blob/master/docs/tutorials/deform_source_mesh_to_target_mesh.ipynb)| [Bundle adjustment](https://github.com/facebookresearch/pytorch3d/blob/master/docs/tutorials/bundle_adjustment.ipynb) |

| <img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/render_textured_mesh.gif" width="310"/> | <img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/camera_position_teapot.gif" width="310" height="310"/>
|:------------------------------------------------------------:|:--------------------------------------------------:|
| [Render textured meshes](https://github.com/facebookresearch/pytorch3d/blob/master/docs/tutorials/render_textured_meshes.ipynb)| [Camera position optimization](https://github.com/facebookresearch/pytorch3d/blob/master/docs/tutorials/camera_position_optimization_with_differentiable_rendering.ipynb)|

| <img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/pointcloud_render.png" width="310"/> | <img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/cow_deform.gif" width="310" height="310"/>
|:------------------------------------------------------------:|:--------------------------------------------------:|
| [Render textured pointclouds](https://github.com/facebookresearch/pytorch3d/blob/master/docs/tutorials/render_colored_points.ipynb)| [Fit a mesh with texture](https://github.com/facebookresearch/pytorch3d/blob/master/docs/tutorials/fit_textured_mesh.ipynb)|

| <img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/densepose_render.png" width="310"/> | <img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/shapenet_render.png" width="310" height="310"/>
|:------------------------------------------------------------:|:--------------------------------------------------:|
| [Render DensePose data](https://github.com/facebookresearch/pytorch3d/blob/master/docs/tutorials/render_densepose.ipynb)| [Load & Render ShapeNet data](https://github.com/facebookresearch/pytorch3d/blob/master/docs/tutorials/dataloaders_ShapeNetCore_R2N2.ipynb)|

| <img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/fit_textured_volume.gif" width="310"/> | <img src="https://raw.githubusercontent.com/facebookresearch/pytorch3d/master/.github/fit_nerf.gif" width="310" height="310"/>
|:------------------------------------------------------------:|:--------------------------------------------------:|
| [Fit Textured Volume](https://github.com/facebookresearch/pytorch3d/blob/master/docs/tutorials/fit_textured_volume.ipynb)| [Fit A Simple Neural Radiance Field](https://github.com/facebookresearch/pytorch3d/blob/master/docs/tutorials/fit_simple_neural_radiance_field.ipynb)|




## Documentation

Learn more about the API by reading the PyTorch3D [documentation](https://pytorch3d.readthedocs.org/).

We also have deep dive notes on several API components:

- [Heterogeneous Batching](https://github.com/facebookresearch/pytorch3d/tree/master/docs/notes/batching.md)
- [Mesh IO](https://github.com/facebookresearch/pytorch3d/tree/master/docs/notes/meshes_io.md)
- [Differentiable Rendering](https://github.com/facebookresearch/pytorch3d/tree/master/docs/notes/renderer_getting_started.md)

### Overview Video

We have created a short (~14 min) video tutorial providing an overview of the PyTorch3D codebase including several code examples. Click on the image below to watch the video on YouTube:

<a href="http://www.youtube.com/watch?v=Pph1r-x9nyY"><img src="http://img.youtube.com/vi/Pph1r-x9nyY/0.jpg" height="225" ></a>

## Development

We welcome new contributions to PyTorch3D and we will be actively maintaining this library! Please refer to [CONTRIBUTING.md](./.github/CONTRIBUTING.md) for full instructions on how to run the code, tests and linter, and submit your pull requests.

## Contributors

PyTorch3D is written and maintained by the Facebook AI Research Computer Vision Team.

In alphabetical order:

* Amitav Baruah
* Steve Branson
* Luya Gao
* Georgia Gkioxari
* Taylor Gordon
* Justin Johnson
* Patrick Labtut
* Christoph Lassner
* Wan-Yen Lo
* David Novotny
* Nikhila Ravi
* Jeremy Reizenstein
* Dave Schnizlein
* Roman Shapovalov
* Olivia Wiles

## Citation

If you find PyTorch3D useful in your research, please cite our tech report:

```bibtex
@article{ravi2020pytorch3d,
    author = {Nikhila Ravi and Jeremy Reizenstein and David Novotny and Taylor Gordon
                  and Wan-Yen Lo and Justin Johnson and Georgia Gkioxari},
    title = {Accelerating 3D Deep Learning with PyTorch3D},
    journal = {arXiv:2007.08501},
    year = {2020},
}
```

If you are using the pulsar backend for sphere-rendering (the `PulsarPointRenderer` or `pytorch3d.renderer.points.pulsar.Renderer`), please cite the tech report:

```bibtex
@article{lassner2020pulsar,
    author = {Christoph Lassner and Michael Zollh\"ofer},
    title = {Pulsar: Efficient Sphere-based Neural Rendering},
    journal = {arXiv:2004.07484},
    year = {2020},
}
```

## News

Please see below for a timeline of the codebase updates in reverse chronological order. We are sharing updates on the releases as well as research projects which are built with PyTorch3D. The changelogs for the releases are available under [`Releases`](https://github.com/facebookresearch/pytorch3d/releases),  and the builds can be installed using `conda` as per the instructions in [INSTALL.md](INSTALL.md).

**[November 2nd 2020]:** PyTorch3D v0.3 released, integrating the pulsar backend.

**[Aug 28th 2020]:**   PyTorch3D v0.2.5 released

**[July 17th 2020]:**   PyTorch3D tech report published on ArXiv: https://arxiv.org/abs/2007.08501

**[April 24th 2020]:**   PyTorch3D v0.2 released

**[March 25th 2020]:**   [SynSin](https://arxiv.org/abs/1912.08804) codebase released using PyTorch3D: https://github.com/facebookresearch/synsin

**[March 8th 2020]:**   PyTorch3D v0.1.1 bug fix release

**[Jan 23rd 2020]:**   PyTorch3D v0.1 released. [Mesh R-CNN](https://arxiv.org/abs/1906.02739) codebase released: https://github.com/facebookresearch/meshrcnn
