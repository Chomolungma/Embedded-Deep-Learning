#**Guide to use docker image file for c3d**
##**target**
load/import existing container of a C3D
create container for C3D

##similar work

  http://qiita.com/daxanya1/items/f04c7f75a6d2ecb92b23
  https://github.com/tensorflow/tensorflow/issues/970
  
##Install Docker Engine

  ref https://docs.docker.com/engine/installation/linux/ubuntulinux/
  
##install nvidia-docker
   
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

##copy CD3
https://github.com/facebook/C3D

ubuntu@SA-ubuntu-GTX1080:/opt$ sudo nvidia-docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
647009cc74c2        nvidia/cuda         "/bin/bash"         52 minutes ago      Up 52 minutes                           docker-c3d

##create docker-c3d
root@SA-ubuntu-GTX1080:/home/ubuntu/Programs/docker4c3d/C3D-master# sudo nvidia-docker run --privileged=true -v /home/ubuntu/Programs/docker4c3d:/opt/docker-share -it --name "docker-c3d" nvidia/cuda /bin/bash

#use docker
##**save/load/export/import**

ref http://tuhrig.de/difference-between-save-and-export-in-docker/  
###Commit your changes and save the container to an image.
ubuntu@SA-ubuntu-GTX1080:/opt$ sudo nvidia-docker commit docker-c3d docker-cuda7.5-c3d-image

$ubuntu@SA-ubuntu-GTX1080:/opt$ sudo nvidia-docker save docker-cuda7.5-c3d-image > /tmp/docker-cuda7.5-c3d-image.tar

###import docker image  
ubuntu@SA-ubuntu-GTX1080:~/Programs/docker4c3d$ sudo nvidia-docker load < ./docker-cuda7.5-c3d.tar

###run imported docker image
   map Ellen's c3d source in /home/Ellen/Programs/docker4c3d <-- win7 can access this folder using winscp
   to  
   Ellen's docker container folder (/opt/docker-share/Ellen) <-- docker container can access this folder  
$sudo nvidia-docker run --privileged=true -v /home/Ellen/Programs/docker4c3d:/opt/docker-share/Ellen -it --name "docker-c3d-Ellen" nvidia/cuda /bin/bash

###Save the mynewimage image to a tar file. 
I will use the /tmp/ directory to save the image but you could easily use a NFS share to make it easier to move the completed tar file.
$ docker save mynewimage > /tmp/mynewimage.tar

####install caffe dependency
***
sudo apt-get update
sudo apt-get --assume-yes install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler; sudo apt-get --assume-yes install --no-install-recommends libboost-all-dev; sudo apt-get --assume-yes install libatlas-base-dev; sudo apt-get --assume-yes install libgflags-dev libgoogle-glog-dev liblmdb-dev  
***

###edit docker4c3d\C3D-master\Makefile.config
to avoid problem of Check failed: error == cudaSuccess (8 vs. 0)  invalid device function

***  
\#CUDA_ARCH := -gencode arch=compute_20,code=sm_20 \\  
\#		-gencode arch=compute_20,code=sm_21 \\  
\#		-gencode arch=compute_30,code=sm_30 \\  
\#		-gencode arch=compute_35,code=sm_35 \\  
		\#-gencode=arch=compute_50,code=sm_50  \\  
		\#-gencode=arch=compute_50,code=compute_50   
CUDA_ARCH := -gencode=arch=compute_52,code=sm_52  \\  
-gencode=arch=compute_52,code=compute_52
***  
root@647009cc74c2:/opt/docker-share/C3D-master# make -j  
root@647009cc74c2:/opt/docker-share/C3D-master/examples/c3d_feature_extraction# sh c3d_sport1m_feature_extraction_frm.sh

####start docker-cuda7.5-c3d  
   map folders 
   docker host' folder ($mkdir -p /home/ubuntu/Programs/docker4c3d) 
   to  
   docker container folder (/opt/C3Da)

sudo nvidia-docker run --privileged=true -v /home/ubuntu/Programs/docker4c3d:/opt/C3Da -it --name "docker-cuda7.5-c3d" nvidia/cuda /bin/bash

###stop docker container  
ref https://www.ctl.io/developers/blog/post/gracefully-stopping-docker-containers/
$sudo docker ps  
$sudo docker stop docker-c3d-ellen  

-----------------
Q: no write permission at current folders and its sub-folder  
A: at current folder, sudo chmod -R a+w ./  

Q: Cannot connect to the Docker daemon. Is the docker daemon running on this host?  
A:  
sudo su -  
service docker start  
docker images

Q: F0603 13:06:47.565624 25295 vol2col.cu:75] Check failed: error == cudaSuccess (8 vs. 0)  invalid device function  
A:   
edit docker4c3d\C3D-master\Makefile.config
***
\#CUDA_ARCH := -gencode arch=compute_20,code=sm_20 \\  
\#		-gencode arch=compute_20,code=sm_21 \\  
\#		-gencode arch=compute_30,code=sm_30 \\  
\#		-gencode arch=compute_35,code=sm_35 \\  
		\#-gencode=arch=compute_50,code=sm_50  \\  
		\#-gencode=arch=compute_50,code=compute_50   
CUDA_ARCH := -gencode=arch=compute_52,code=sm_52  \\  
-gencode=arch=compute_52,code=compute_52
***

C3D-master# make -j

Q: how to enable remote GUI access from windows rdp to ubuntu machine?
A: ref http://c-nergy.be/blog/?p=5874 
   $sudo apt-get udpate  
   $sudo apt-get install xrdp  
   $sudo apt-get install lxde  
   $echo lxsession -s LXDE -e LXDE > ~/.xsession 
   use win7 remote desktop to connect ubuntu's IP
   


---------------

