**Guide to use docker image file for c3d**

##Convention  
$cmd@docker-host <-$   
\#cmd@docker-container <-\#  
Replace "/home/ubuntu" with "/home/your-user-name"

##Target
Refer to the illustration at <a href ="https://github.com/NVIDIA/nvidia-docker/blob/master/README.md">Nvidia Docker</a>. 
<p>Our targets are as follow:  
1) Setup container1 for c3d for user1  
2) Save container1   
3) Load container1    

##Similar Work  
  <a href ="http://qiita.com/daxanya1/items/f04c7f75a6d2ecb92b23">Qiita - daxanya1</a>  
  <a href ="https://github.com/tensorflow/tensorflow/issues/970">Tensorflow GitHub</a>  
  
##Tested System
Ubuntu 14.04.3  
docker engine 1.11.2 

##Install/Download  
###Docker Engine <- skip if already installed  
ref (https://docs.docker.com/engine/installation/linux/ubuntulinux/)  
###Nvidia-docker <- skip if already installed  
ref https://hub.docker.com/r/skydjol/nvidia-docker/  
ref https://github.com/NVIDIA/nvidia-docker/wiki/nvidia-docker-plugin	
-Download https://github.com/NVIDIA/nvidia-docker/archive/master.zip to ~/Programs/nvidia-docker/master.zip 
at ~/Programs/nvidia-docker
	`$ unzip master.zip; cd master; sudo make -j; sudo make install; nvidia-docker run --rm nvidia/cuda nvidia-smi`  
at another terminal  
	`$ sudo nvidia-docker-plugin`
###C3D  
ref https://github.com/facebook/C3D
<p>download https://github.com/facebook/C3D/archive/master.zip to /home/ubuntu/Programs/docker4c3d/C3D-master.zip
at /home/ubuntu/Programs/docker4c3d/
	`$ unzip C3D-master.zip` <- later we map resulted /C3D-master folder to container1's folder

##Use docker  
###Create container1 to run downloaded C3D
<b> at ubuntu terminal-1  <\b>
	`$sudo nvidia-docker-plugin` <- ref https://github.com/NVIDIA/nvidia-docker/wiki/nvidia-docker-plugin  
	
<b> at terminal-2 <\b> <- notice long command  
Replace above proxy-ip 1.2.3.4 with ip returned by $ ping proxy.your.company.com  
replace below "home/docker-share/ubuntu" with "/home/docker-share/your-username"
Replace above proxy-port 5678 with port you set in internet browser  
***
`$ sudo nvidia-docker run --privileged=true --env http_proxy="http://1.2.3.4:5678" -v /home/ubuntu/Programs/docker4c3d:/opt/docker-share/ubuntu -it --name "container-name" nvidia/cuda /bin/bash`  
*** 

```
	cd /opt/docker-share/ubuntu    
	make -j  <-check error's keyword at Q&A  
	cd master/examples/c3d_feature_extraction; sh c3d_sport1m_feature_extraction_frm.sh  
```
	
###Commit/Save/Load container1 
ref http://tuhrig.de/difference-between-save-and-export-in-docker/  
	<-to check why image-name.tar about 2Gbyte  
	<-if not saved, lost container changes when stop container or reboot  
```
	$ sudo nvidia-docker commit container-name image-name    
	$ sudo nvidia-docker image-name > /opt/docker-share/ubuntu/image-name.tar  
	$ sudo nvidia-docker load < /home/ubuntu/Programs/docker4c3d/image-name.tar  
	$ sudo nvidia-docker run --privileged=true --env http_proxy="http://1.2.3.4:5678" -v /home/ubuntu/Programs/docker4c3d:/opt/docker-share/ubuntu -it --name "container-name" nvidia/cuda /bin/bash  
```	

###Stop docker container  
ref https://www.ctl.io/developers/blog/post/gracefully-stopping-docker-containers/  
```
	$ sudo docker ps -a
	$ sudo docker stop container-name
```

##Q&A
-----------------
Q: no write permission at current folders and its sub-folder  
A: At current folder, sudo chmod -R a+w ./  

Q: Error: Cannot connect to the Docker daemon. Is the docker daemon running on this host?      
A: Add sudo in front of nvidia-docker
   <p>Wrong: "nvidia-docker"
   <p>Correct: "sudo nvidia-docker"

Q: How do I install caffe dependencies in c3d?  
A:
```
# If can't update, check proxy setting as shown above  
$ sudo apt-get update

# Install the library dependencies
$ sudo apt-get --assume-yes install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler; sudo apt-get --assume-yes install --no-install-recommends libboost-all-dev; sudo apt-get --assume-yes install libatlas-base-dev; sudo apt-get --assume-yes install libgflags-dev libgoogle-glog-dev liblmdb-dev 
```

Q: How do I solve error == cudaSuccess (8 vs. 0)  invalid device function?      
A: Edit docker4c3d\C3D-master\Makefile.config    
***
\#filename docker4c3d\C3D-master\Makefile.config  
\#CUDA_ARCH := -gencode arch=compute_20,code=sm_20 \\  
\#\...  
\#-gencode=arch=compute_50,code=compute_50  
CUDA_ARCH := -gencode=arch=compute_52,code=sm_52  \\  
-gencode=arch=compute_52,code=compute_52  
***  

Q:How do I enable remote GUI access from windows rdp to ubuntu machine?    
A: ref http://c-nergy.be/blog/?p=5874   
```
   $ sudo apt-get update  
   $ sudo apt-get install xrdp  
   $ sudo apt-get install lxde  
   $ echo lxsession -s LXDE -e LXDE > ~/.xsession 
   use win7 remote desktop to connect ubuntu's IP  
```

Q: "\#sudo apt-get update" fail behind proxy, work without proxy, why?      
A: Set proxy when start a container $ docker run --env http_proxy="http://1.2.3.4:5678"   
edit /etc/default/docker; then $ sudo service docker restart<- this method not effecive current system I tested

Q: How do I attach to a running container?      
A:
```
$ sudo nvidia-docker attach container-name  <-if error "cannot attach stopped container, start it first", refer below  
$ sudo nvidia-docker start container-name  
$ sudo attach docker-attach container-name  
```

Q: How do I check the version of ubuntu & docker-engine?      
A:
```
$ cat /etc/issue  
$ sudo docker version
```

Q: How do I share files between docker container, docker host and windows PC?      
A: map container folder to host folder, read/write between win7 and host-folder using winscp  
ref https://winscp.net/eng/docs/guide_install

---------------

