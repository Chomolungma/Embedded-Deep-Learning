Guide to use docker image file for c3d

caffe

reference

similar work

  http://qiita.com/daxanya1/items/f04c7f75a6d2ecb92b23
  
Install Docker Engine

  ref https://docs.docker.com/engine/installation/linux/ubuntulinux/
  
nvidia-docker
   
    https://hub.docker.com/r/skydjol/nvidia-docker/
    download from https://github.com/NVIDIA/nvidia-docker/archive/master.zip to ubuntu's ~/Programs/nvidia-docker
    unzip ~/Programs/nvidia-docker$ unzip master.zip
    compile nvidia-docker: make -j
    install nvidia-docker: make install
    run nvidia-docker-plugin: nvidia-docker-plugin 

C3D
https://github.com/facebook/C3D

install caffe dependency
sudo apt-get --assume-yes install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler; sudo apt-get install --no-install-recommends libboost-all-dev; sudo apt-get --assume-yes install libatlas-base-dev; sudo apt-get --assume-yes install libgflags-dev libgoogle-glog-dev liblmdb-dev

start docker-cuda7.5-c3d

