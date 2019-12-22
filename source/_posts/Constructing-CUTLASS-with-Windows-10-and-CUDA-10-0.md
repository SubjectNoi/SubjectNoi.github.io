---
title: Constructing CUTLASS with Windows 10 and CUDA 10.0
date: 2019-01-28 10:48:44
tags: [C, C++, CUDA, CUTLASS]
categories: Constructing environment
---

# About CUTLASS

CUTLASS is a template library developed by Nvidia with CUDA 10.0 aiming to deal with Linear Algebra Computation. You can find CUTLASS [here](https://github.com/NVIDIA/CUTLASS). The readme.md of the original project is based on unix family OS, This article will introduce how to construct CUTLASS on windows 10.

# Parperation

* Windows 10 64-bit
* CUDA 10.0
* Visual Studio 2017
* CMAKE (Version > 3.10)
* git

Please make sure all the CUDA component are in the system path, and test with related command: nvcc, cl, etc.

# Constructing CUTLASS

Since this project use test suite from google named gtest, so to run the unit test in it, gtest is essential.

First, get the repo:
```
git clone https://github.com/NVIDIA/CUTLASS
```
Second, get the test sub module:
```
git submodule update --init --recursive
```
Then, create the build target folder and enter in:
```
mkdir build && cd build
```
It's time to construct, different with the official document, you should specify the generator if you build with Windows 10, so, some adjustment should be taken:
```
cmake -G "Visual Studio 15 2017 Win64" ..
```
The "Win64" at last is quite important. 

If you make this repo in windows 10, it is quite possible that pthread is not installed on your PC, and you will see the warning information like:
```
-- Looking for pthread.h
-- Looking for pthread.h - not found
```
This can be ignore. 

After that, you should see complete tree structure in your working dir like:
/build--/CMakeFiles
/-------/examples
/-------/tools
/-------/x64
/-----CUTLASS.sln
/-----.(Some project generated files)
/-----.
/-----.
Then, open the **CUTLASS.sln** with Visual Studio 2017, right click on the project **ALL_BUILD**, select build, and wait.

At last, you should see executable file in /tools/test/unit/debug/cutlass_unit_test.exe, run it!