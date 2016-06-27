# Installation of Caffe

```
$ sudo add-apt-repository universe
$ sudo apt-get update –y
$ sudo apt-get install cmake –y

# General Dependencies
$ sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler –y
$ sudo apt-get install --no-install-recommends libboost-all-dev –y

# BLAS
$ sudo apt-get install libatlas-base-dev –y

# Remaining Dependencies
$ sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev –y

# Change Directory
$ cd Programs/caffe-caffe-0.14-fp16

# Copy Makefile.config.example
$ cp Makefile.config.example Makefile.config

# Use only 3 cores on L4T 23.1 install
# 4 cores hangs system
$ make -j3 all

# Run the tests to make sure everything works
$ make -j3 runtest
```
