# Adapting rmm-diis.cu in VASP to CUDA version over 10

## Problem
When compile ```vasp_gpu``` with CUDA 10 or later versions, there will be errors:
```bash
rmm-diis.cu(45): error: texture is not a template
  texture<uint2> texX;
  ^

rmm-diis.cu(46): error: texture is not a template
  texture<uint2> texY;
  ^

rmm-diis.cu(293): error: identifier "cudaBindTexture" is undefined
          if ((cudaStat=cudaBindTexture (&texXOfs,texX,W1_CR,sizeX*sizeof(W1_CR[0]))) !=
                        ^

rmm-diis.cu(301): error: identifier "cudaUnbindTexture" is undefined
              cudaUnbindTexture (texX);
              ^

rmm-diis.cu(386): error: identifier "cudaUnbindTexture" is undefined
          if ((cudaStat = cudaUnbindTexture (texX)) != cudaSuccess) {
                          ^
```

## Solution
Replace src/CUDA/rmm-diis.cu with file [rmm-diis.cu](rmm-diis.cu):
```bash
wget https://raw.githubusercontent.com/abhpc/vasp-adapt-cuda-10/refs/heads/main/rmm-diis.cu
\cp -Rf rmm-diss.cu src/CUDA/rmm-diss.cu
```
