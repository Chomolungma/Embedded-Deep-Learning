#**Guide to use docker image file for c3d**

##command convention  
$cmd@docker-host  
\#cmd@docker-container

##target
refer to picture at https://github.com/NVIDIA/nvidia-docker/blob/master/README.md  
our targets are
1)setup container1 for c3d for user1  
2)save container1   
3)load container1    

##similar work  
  http://qiita.com/daxanya1/items/f04c7f75a6d2ecb92b23  
  https://github.com/tensorflow/tensorflow/issues/970  
  
##tested system
Ubuntu 14.04.3  
docker engine 1.11.2 

##install/download  
###docker engine <- skip if already installed  
ref (https://docs.docker.com/engine/installation/linux/ubuntulinux/)  
###invidia-docker  <- skip if already installed  
ref https://hub.docker.com/r/skydjol/nvidia-docker/  
ref https://github.com/NVIDIA/nvidia-docker/wiki/nvidia-docker-plugin	
-download https://github.com/NVIDIA/nvidia-docker/archive/master.zip to ~/Programs/nvidia-docker/master.zip 
at ~/Programs/nvidia-docker
	$unzip master.zip; cd master; sudo make -j; sudo make install; nvidia-docker run --rm nvidia/cuda nvidia-smi  
at another terminal  
	$nvidia-docker-plugin
###CD3  
ref https://github.com/facebook/C3D
download https://github.com/facebook/C3D/archive/master.zip to /home/ellen/Programs/docker4c3d/master.zip
at /home/ellen/Programs/docker4c3d/
	$unzip master.zip <- later we map resulted /master folder to container1's folder

##use docker  
###create container1 to run downloaded C3D
at ubuntu terminal-1  
	$nvidia-docker-plugin <- ref https://github.com/NVIDIA/nvidia-docker/wiki/nvidia-docker-plugin
at terminal-2  <-- notice long command
  	$sudo nvidia-docker run --privileged=true --env http_proxy="http://1.2.3.4:5678" -v /home/ubuntu/Programs/docker4c3d:/opt/docker-share/ubuntu -it --name "container-name" nvidia/cuda /bin/bash  
  		replace above proxy-ip 1.2.3.4 with ip returned by $ping proxy.your.company.com  
  		replace above proxy-port 5678 with port you set in internet browser  
	\#cd /opt/docker-share/ubuntu;  
	#make -j  
	#cd master/examples/c3d_feature_extraction; sh c3d_sport1m_feature_extraction_frm.sh
	
###save/load container1 
ref http://tuhrig.de/difference-between-save-and-export-in-docker/ 
	$sudo nvidia-docker commit container-name image-name <-if not saves, lost container changes when stop container or reboot
	$sudo nvidia-docker image-name > /opt/docker-share/ubuntu/image-name.tar <-to check why image-name.tar about 2Gbyte
###import docker image  
	~/Programs/docker4c3d$sudo nvidia-docker load < ./image-name.tar  
###run imported docker image
	$sudo nvidia-docker run --privileged=true --env http_proxy="http://1.2.3.4:5678" -v /home/ubuntu/Programs/docker4c3d:/opt/docker-share/ubuntu -it --name "container-name" nvidia/cuda /bin/bash  
	  	replace proxy-ip 1.2.3.4 with ip returned by $ping proxy.your.company.com  
	  	replace proxy-port 5678 based on internet browser setting  
to save changes as image, refer save/load container1  


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

Q: how to install caffe dependencies in c3d?
A:
	\#sudo apt-get update <-if can't update, check proxy setting above
	\#sudo apt-get --assume-yes install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler; sudo apt-get --assume-yes install --no-install-recommends libboost-all-dev; sudo apt-get --assume-yes install libatlas-base-dev; sudo apt-get --assume-yes install libgflags-dev libgoogle-glog-dev liblmdb-dev 

Q: how to solve error == cudaSuccess (8 vs. 0)  invalid device function?
A:   
edit docker4c3d\C3D-master\Makefile.config
	\#filename docker4c3d\C3D-master\Makefile.config
	\#CUDA_ARCH := -gencode arch=compute_20,code=sm_20 \\  
	\#\...  
	\#-gencode=arch=compute_50,code=compute_50   
	CUDA_ARCH := -gencode=arch=compute_52,code=sm_52  \\  
	-gencode=arch=compute_52,code=compute_52  

Q: how to enable remote GUI access from windows rdp to ubuntu machine?
A: ref http://c-nergy.be/blog/?p=5874 
   $sudo apt-get udpate  
   $sudo apt-get install xrdp  
   $sudo apt-get install lxde  
   $echo lxsession -s LXDE -e LXDE > ~/.xsession 
   use win7 remote desktop to connect ubuntu's IP  

Q: "\#sudo apt-get update" fail behind proxy, work without proxy
A: set proxy when start a container $docker run --env http_proxy="http://1.2.3.4:5678" 
edit /etc/default/docker; then $sudo service docker restart<- this method not effecive current system I tested

Q: how to attach to a running container
A:	$sudo nvidia-docker attach container-name
	if error "You cannot attach to a stopped container, start it first"
	$sudo nvidia-docker start container-name
	$sudo attach docker-attach container-name

Q: how to check version of ubuntu & docker-engine?
A:	$cat /etc/issue
  	$sudo docker version

Q:how to share files between docker container, docker host and windows PC?  
A:	map container folder to host folder, read/write between win7 and host-folder using winscp  
		ref https://winscp.net/eng/docs/guide_install

---------------

