Guide to use docker image file for C3D
=======================================

  * [Convention](#convention)
  * [Target](#target)
  * [Related Work](#related-work)
  * [Tested System](#tested-system)
  * [Install/Download](#installdownload)
    * [Docker Engine](#docker-engine)
    * [Nvidia Docker](#nvidia-docker)
    * [C3D](#c3d)
  * [Use docker](#use-docker)
    * [Create container1 to run downloaded C3D](#create-container1-to-run-downloaded-c3d)
    * [Commit/Save/Load container1](#commitsaveload-container1)
    * [Stop Docker Container](#stop-docker-container)
    * [Q&A](#qa)

****
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

##Related Work  
  [Qiita - daxanya1](http://qiita.com/daxanya1/items/f04c7f75a6d2ecb92b23)  
  [Tensorflow GitHub](https://github.com/tensorflow/tensorflow/issues/970)  
  
##Tested System
* Ubuntu 14.04.3  
* Docker engine 1.11.2 

##Install/Download/Uninstall  
###Docker Engine 
<- skip if already installed  
ref (https://docs.docker.com/engine/installation/linux/ubuntulinux/)  

####install
```
1. To check your kernel version
$ uname -r

2. Update your apt sources
$ sudo apt-get update

3. Update package information, ensure that APT works with the https method, and that CA certificates are installed
$ sudo apt-get install apt-transport-https ca-certificates

4. Add new GPG key
$ sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D

5. Open the /etc/apt/sources.list.d/docker.list file in your favorite editor
   If the file doesn’t exist, create it.
   
6. Remove any existing entries.

7. Add an entry for Ubuntu operating system
$ deb https://apt.dockerproject.org/repo ubuntu-trusty main

8. Press Ctrl + X, followed by pressing Y and enter 

9. Update the APT package index
$ sudo apt-get update
   
10. Purge the old repo if it exists
$ sudo apt-get purge lxc-docker
   
11. Verify that APT is pulling from the right repository
$ apt-cache policy docker-engine

12. Update your package manager
$ sudo apt-get update
   
13. Install the recommended package
$ sudo apt-get install linux-image-extra-$(uname -r)

14. Install apparmor
$ sudo apt-get install apparmor

15. Update your APT package index
$ sudo apt-get update

16. Install Docker
$ sudo apt-get install docker-engine

17. Start the docker daemon
$ sudo service docker start

18. Verify docker is installed correctly
$ sudo docker run hello-world
```

####uninstall
sudo apt-get remove docker-engine

###Nvidia Docker 
####install
<- skip if already installed  
ref:      https://hub.docker.com/r/skydjol/nvidia-docker/  
          https://github.com/NVIDIA/nvidia-docker/wiki/nvidia-docker-plugin	
<p>Download: https://github.com/NVIDIA/nvidia-docker/archive/master.zip to ~/Programs/nvidia-docker/master.zip 
at ~/Programs/nvidia-docker
	`$ unzip master.zip; cd master; sudo make -j; sudo make install;` 
	`$ sudo nvidia-docker run --rm nvidia/cuda nvidia-smi`  
at another terminal  
	`$ sudo nvidia-docker-plugin`
####uninstall
at ~/Programs/nvidia-docker/nvidia-docker-master
`$sudo make uninstall`

###C3D  
ref https://github.com/facebook/C3D
<p>download https://github.com/facebook/C3D/archive/master.zip to /home/ubuntu/Programs/docker4c3d/C3D-master.zip
At /home/ubuntu/Programs/docker4c3d/
	<p>`$ unzip C3D-master.zip` <- later we map resulted /C3D-master folder to container1's folder
At /home/ubuntu/Programs/docker4c3d/C3D-master
Copy or duplicate Makefile.config.example to Makefile.config
`$ cp Makefile.config.example Makefile.config`
##Use docker  
###Create container1 to run downloaded C3D
<b>At ubuntu terminal-1</b>
	`$ sudo nvidia-docker-plugin` <- ref https://github.com/NVIDIA/nvidia-docker/wiki/nvidia-docker-plugin  
	
<b>At ubuntu terminal-2</b> <- notice long command  
replace below
<p>
1)proxy-ip 1.2.3.4 with ip returned by $ ping proxy.your.company.com  
2)"home/docker-share/ubuntu" with "/home/docker-share/your-username"
3)"home/ubuntu" with "/home/your-username"
4)proxy-port 5678 with port you set in internet browser 

***
`$ sudo nvidia-docker run --privileged=true --env http_proxy="http://1.2.3.4:5678" -v /home/ubuntu/Programs/docker4c3d:/opt/docker-share/ubuntu -it --name "container-name" nvidia/cuda /bin/bash`  
*** 

```
	#cd /opt/docker-share/ubuntu    
	#cd C3D-master  
	#make -j  <-check error's keyword at Q&A  
	#cd examples/c3d_feature_extraction; sh c3d_sport1m_feature_extraction_frm.sh  
```
	
###Commit/Save/Load container1 
ref http://tuhrig.de/difference-between-save-and-export-in-docker/  
	<-to check why image-name.tar about 2Gbyte  
	<-if not saved, lost container changes when stop container or reboot  
```
	$ sudo nvidia-docker commit container-name image-name    
	$ sudo nvidia-docker save image-name > /home/ubuntu/Programs/docker4c3d/image-name.tar  
	$ sudo docker rmi images-name <- check deleted
	$ sudo nvidia-docker load < /home/ubuntu/Programs/docker4c3d/image-name.tar  
	$ sudo docker rmi images-name <- check loaded
	$ sudo nvidia-docker run --privileged=true --env http_proxy="http://1.2.3.4:5678" -v /home/ubuntu/Programs/docker4c3d:/opt/docker-share/ubuntu -it --name "container-name" image-name /bin/bash  
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
```
Change
\#filename docker4c3d\C3D-master\Makefile.config  
\#CUDA_ARCH := -gencode arch=compute_20,code=sm_20 \\  
\#\...  
\#-gencode=arch=compute_50,code=compute_50  

To
CUDA_ARCH := -gencode=arch=compute_52,code=sm_52 -gencode=arch=compute_52,code=compute_52  
 
# cd ..
# cd ..
# make clean
# make -j
``` 

Q:How do I enable remote GUI access from windows rdp to ubuntu machine?    
A: ref http://c-nergy.be/blog/?p=5874   
```
   $ sudo apt-get update  
   $ sudo apt-get install xrdp  
   $ sudo apt-get install lxde  
   $ echo lxsession -s LXDE -e LXDE > ~/.xsession 
   use win7 remote desktop to connect ubuntu's IP  
```

Q: `#sudo apt-get update` fail behind proxy, work without proxy, why?      
A: Set proxy when start a container `$ docker run --env http_proxy="http://1.2.3.4:5678"`   
edit /etc/default/docker; then `$ sudo service docker restart`<- this method not effecive current system I tested

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

Q: How do I solve this error?
Error: listen tcp 127.0.0.1:3476: bind: address already in use    
A: 
```
$ ps aux | grep nvidia-docker-plugin

Display
root     xxxxx  0.0  0.0  75368  4004 pts/32   S+   11:44   0:00 sudo nvidia-docker-plugin
$ sudo kill xxxxx

# To check if the program is still running
$ ps aux | grep nvidia-docker-plugin
```
Q: My IP address is not showing. How do I find my IP address?
<p>A: 
```
$ sudo ipconfig eth0 down
$ sudo ipconfig eth0 up
```

---------------

