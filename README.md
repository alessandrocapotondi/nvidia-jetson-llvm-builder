# Nvidia Jetson Nano LLVM Builder

Builder script for Clang/LLVM10 compiler for Nvidia Jetson Nano (could be extended to other Jetson boards) with OpenMP 4.5 offloading support. The script is created to be executed directly in the Nvidia Jetson Nano. Larger SWAP memory is recommended (see below).

## Current Target
* Clang/LLVM v10.0.0
* Supported Compute Capabilities: `53,62,72`
* Default `CLANG_OPENMP_NVPTX_DEFAULT_ARCH` is `sm_53` (Compute Capability 5.3)

You can extend the Compute Capabilities setting the `CLANG_OPENMP_NVPTX_DEFAULT_ARCH` and `LIBOMPTARGET_NVPTX_COMPUTE_CAPABILITIES` environmental variables.

# How-to Use
* Build Clang/LLVM
```
./jetson-llvm-builder [-s $LLVM_SRC] [-i $LLVM_PATH]
```

The script will download the required Clang/LLVM sources in the `$LLVM_SRC` (default: `/$HOME`). The default value for `$LLVM_PATH` is `/usr/local/`.

* Use the new compiler
Following environment variables need to be set before using Clang/LLVM
```
export PATH=$LLVM_PATH:$PATH
export LD_LIBRARY_PATH=$LLVM_PATH/libexec:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=$LLVM_PATH/lib:$LD_LIBRARY_PATH
export LIBRARY_PATH=$LLVM_PATH/libexec:$LIBRARY_PATH
export LIBRARY_PATH=$LLVM_PATH/lib:$LIBRARY_PATH
export MANPATH=$LLVM_PATH/share/man:$MANPATH
export C_INCLUDE_PATH=$LLVM_PATH/include:$C_INCLUDE_PATH
export CPLUS_INCLUDE_PATH=$LLVM_PATH/include:CPLUS_INCLUDE_PATH
```

> Nvidia Jetson Nano has 4 GB of DDR4 memory, plus, by default, it has 2GB of SWAP. Memory usage during the build of Clang/LLVM may be larger, thus is recommended to increase the SWAP partition to 8-16GB. You can do it following this tutorial: https://www.jetsonhacks.com/2019/11/28/jetson-nano-even-more-swap/
