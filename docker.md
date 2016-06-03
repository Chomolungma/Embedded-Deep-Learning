Guide to use docker image file for c3d

caffe

reference

similar work

  http://qiita.com/daxanya1/items/f04c7f75a6d2ecb92b23
  https://github.com/tensorflow/tensorflow/issues/970
  
Install Docker Engine

  ref https://docs.docker.com/engine/installation/linux/ubuntulinux/
  
nvidia-docker
   
    https://hub.docker.com/r/skydjol/nvidia-docker/
    download from 
       https://github.com/NVIDIA/nvidia-docker/archive/master.zip 
    store at ubuntu's 
       ~/Programs/nvidia-docker/master.zip 
    unzip 
       ~/Programs/nvidia-docker$ unzip master.zip
    compile nvidia-docker: 
       sudo make -j
    install nvidia-docker: 
       sudo make install
    run nvidia-docker-plugin: 
       nvidia-docker-plugin 
    
    Q: uvm issue 
    A: https://gist.github.com/Brainiarc7/bb4b3367acb673ab6c7e 
       http://askubuntu.com/questions/595486/ubuntu-14-04-nvidia-proprietry-346-drivers
       sudo apt-get install nvidia-346 nvidia-settings nvidia-prime              <---- wrong method
      sudo reboot

C3D
https://github.com/facebook/C3D

import docker image
ubuntu@SA-ubuntu-GTX1080:~/Programs/docker4c3d$ sudo nvidia-docker load < ./docker-cuda7.5-c3d.tar

export docker image
	
$ docker commit 3a09b2588478 mynewimage

Save the mynewimage image to a tar file. 
I will use the /tmp/ directory to save the image but you could easily use a NFS share to make it easier to move the completed tar file.
$ docker save mynewimage > /tmp/mynewimage.tar

install caffe dependency

sudo apt-get --assume-yes install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler; sudo apt-get install --no-install-recommends libboost-all-dev; sudo apt-get --assume-yes install libatlas-base-dev; sudo apt-get --assume-yes install libgflags-dev libgoogle-glog-dev liblmdb-dev

start docker-cuda7.5-c3d

   map folders 
   docker host' folder ($mkdir -p /home/ubuntu/Programs/docker4c3d) 
   to  
   docker container folder (/opt/C3Da)

sudo nvidia-docker run --privileged=true -v /home/ubuntu/Programs/docker4c3d:/opt/C3Da -it --name "docker-cuda7.5-c3d" nvidia/cuda /bin/bash

-----------------
Q: no write permission at current folders and its sub-folder

A: at current folder, sudo chmod -R a+w ./

Q: Cannot connect to the Docker daemon. Is the docker daemon running on this host?
A:
sudo su -
service docker start
docker images

---------------

