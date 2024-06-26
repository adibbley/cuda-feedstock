# Guide for Maintainers of CUDA recipes

This guide is intended for maintainers of the CUDA packages themselves.

## Rationale for split packages

In addition to the standardized dev/static division of libraries, some packages are also divided into multiple pieces for more specialized reasons.

### nvcc split

While the `nvcc` compiler natively supports cross-compilation, a target-specific headers are still needed.
To support this, the `nvcc` compiler is split into a couple of feedstocks, [`cuda-nvcc`](https://github.com/conda-forge/cuda-nvcc-feedstock/) and [`cuda-nvcc-impl`](https://github.com/conda-forge/cuda-nvcc-impl-feedstock/).
These packages split the files such that we can have the compiler package be dependent exclusively on the platform for which it is compiled while the `cuda-nvcc-impl` package is dependent only on the cross-compilation target and includes the required headers (and other files) such that compilation will succeed.
This way, the two packages may be updated or changed in parallel and will interoperate properly in cross-compilation environments.
