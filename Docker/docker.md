Guide to use docker image file for C3D
=======================================

  * [Convention](#convention)
  * [Target](#target)
  * [Related Work](#related-work)
  * [Environment Setup](#environment-setup)
  * [Install/Download/Uninstall](#installdownloaduninstall)
    * [Docker Engine](#docker-engine)
    * [Nvidia Docker](#nvidia-docker)
    * [C3D](#c3d)
  * [Use docker](#use-docker)
    * [Create container1 to run downloaded C3D](#create-container1-to-run-downloaded-c3d)
    * [Commit/Save/Load container1](#commitsaveload-container1)
    * [Stop Docker Container](#stop-docker-container)
    * [Add Multiple Users](#add-multiple-users)
    * [Create a docker group](#create-a-docker-group)
  * [Build your own images](#build-your-own-images)
    * [SSH Client Display ssh server GUI](#ssh-client-display-ssh-server-gui)
  * [Q&A](#qa)
  
****
##Convention
At Docker-Host,
<br>Symbol: $
<br>Example: <b>$</b>cmd@docker-host

At Docker-Container, 
<br>Symbol: \#
<br>Example: <b>#</b>cmd@docker-container

Note: Replace "/home/<b>ubuntu</b>" with "/home/<b>your-user-name</b>"

##Target
For more information, refer to the illustration at [Nvidia Docker](https://github.com/NVIDIA/nvidia-docker/blob/master/README.md).

Our targets are as follow:  
* Install Docker Engine and Nvidia Docker
* Setup container1 for C3D for user1
* Save container1
* Load container1

##Related Work  
* [Qiita - daxanya1](http://qiita.com/daxanya1/items/f04c7f75a6d2ecb92b23)  
* [Tensorflow GitHub](https://github.com/tensorflow/tensorflow/issues/970)  
  
##Environment Setup
* Ubuntu 14.04.3  
* Docker engine 1.11.2 

##Install/Download/Uninstall  
###Docker Engine 
Please refer to [Installation of Docker Engine](https://docs.docker.com/engine/installation/linux/ubuntulinux/) for more information. 

####Install
-> skip if already installed  
```
1. To check your kernel version
$ uname -r
* Docker requires kernel to be 3.10 at minimum.

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

####Uninstall
To uninstall the Docker package:
<br>`$ sudo apt-get purge docker-engine`

To uninstall the Docker package and dependencies that are no longer needed:
<br>`$ sudo apt-get autoremove --purge docker-engine`

The above commands will not remove images, containers, volumes, or user created configuration files on your host. 
<br>To delete all images, containers, and volumes run the following command:
<br>`$ rm -rf /var/lib/docker`

###Nvidia Docker 
Please refer to [Installation of Nvidia Docker](https://hub.docker.com/r/skydjol/nvidia-docker/) and [Nvidia Docker Github](https://github.com/NVIDIA/nvidia-docker/wiki/nvidia-docker-plugin) for more information. 

####Install
-> skip if already installed
<br>1. Download https://github.com/NVIDIA/nvidia-docker/archive/master.zip to ~/Programs/nvidia-docker/master.zip
<br>2. At ~/Programs/nvidia-docker,
<br>
```
$ unzip nvidia-docker-master.zip
$ cd nvidia-docker-master
$ sudo make -j
$ sudo make install
$ sudo nvidia-docker-plugin
```
<br>3. Open a new another terminal,
<br>`$ sudo nvidia-docker run --rm nvidia/cuda nvidia-smi`

####Uninstall
At ~/Programs/nvidia-docker/nvidia-docker-master,
<br>`$ sudo make -C ~/Programs/nvidia-docker/nvidia-docker-master/tools uninstall`

###C3D  
For more information, please refer to [C3D](https://github.com/facebook/C3D).

####Install
<br>1. Download https://github.com/facebook/C3D/archive/master.zip to /home/ubuntu/Programs/docker4c3d/C3D-master.zip
<br>2. At /home/ubuntu/Programs/docker4c3d/,
    <br>`$ unzip C3D-master.zip; cd C3D-master` <- later we map resulted /C3D-master folder to container1's folder
<br>3. At /home/ubuntu/Programs/docker4c3d/C3D-master, copy or duplicate Makefile.config.example to Makefile.config.
    <br>`$ cp Makefile.config.example Makefile.config`
        
##Use docker  
###Create container1 to run downloaded C3D
<b>At ubuntu terminal-1</b>  
   `$ sudo nvidia-docker-plugin` <- ref https://github.com/NVIDIA/nvidia-docker/wiki/nvidia-docker-plugin  
	
<b>At ubuntu terminal-2</b> <- notice long command  
Replace below
<p>
<p>1) proxy-ip 1.2.3.4 with ip returned by $ ping proxy.your.company.com  
<p>2) "home/docker-share/<b>ubuntu</b>" with "/home/docker-share/<b>your-username</b>"
<p>3) "home/<b>ubuntu</b>" with "/home/<b>your-username</b>"
<p>4) proxy-port 5678 with port you set in internet browser 
```
$ sudo nvidia-docker run --privileged=true --env http_proxy="http://1.2.3.4:5678" -v /home/ubuntu/Programs/docker4c3d:/opt/docker-share/ubuntu -it --name "container-name" nvidia/cuda /bin/bash  
# cd /opt/docker-share/ubuntu    
# cd C3D-master  
# make -j  <-check error's keyword at Q&A  
# cd examples/c3d_feature_extraction; sh c3d_sport1m_feature_extraction_frm.sh  
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
$ sudo docker images-name <- check loaded
$ sudo nvidia-docker run --privileged=true --env http_proxy="http://1.2.3.4:5678" -v /home/ubuntu/Programs/docker4c3d:/opt/docker-share/ubuntu -it --name "container-name" image-name /bin/bash  
```	

Batch commands
src: (http://honeyco.nyc/blog/docker-tips-and-tricks/)
Sometimes it can be quicker to operate on multiple docker containers at once, especially while testing a new container to get the parameters correct.

Remove all containers of a given image:
```
docker rm `docker ps -a | grep 0fa4de | cut -f1 -d" "`
# also this format uses xargs instead of backticks
docker ps -a | grep 0fa4de | cut -d ' ' -f 1 | xargs docker rm

# or if you need to stop them before removing replace rm with kill:
docker ps -a | grep 0fa4de | cut -d ' ' -f 1 | xargs docker kill
docker ps -a | grep 0fa4de | cut -d ' ' -f 1 | xargs docker rm
```

Remove stopped containers:
`docker ps -a | grep Exit | cut -d ' ' -f 1 | xargs docker rm`

You can use similar techniques for deleting images (though removing multiple images is less common):
`docker ps -a | grep string-of-text | cut -d ' ' -f 1 | xargs docker rmi`


###Stop docker container  
ref https://www.ctl.io/developers/blog/post/gracefully-stopping-docker-containers/  
```
$ sudo docker ps -a
$ sudo docker stop container-name
```

###Add Multiple Users
For more information, please refer to [how to add and delete users on ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-an-ubuntu-14-04-vps).
<p>To add user:
<br>`$ sudo adduser newuser`
<p>To grant Privileges:
<br>`$ sudo visudo`
<p>Search for the line that looks like this:
<br>`root    ALL=(ALL:ALL) ALL`

Using the format of the root user, change root to the new user that you would like to give sudo privileges to:
<br>`root    ALL=(ALL:ALL) ALL`
<br>`newuser ALL=(ALL:ALL) ALL`
<br>Press Ctrl + X, followed by pressing Y and enter to save and exit.

For testing,
<br>When signed in as the new user, try to execute commands as your regular user by typing commands as normal:
<br>`$ some_command`

and execute the same command with administrative privileges by typing sudo ahead of the command:
<br>`$ sudo some_command`

###Create a docker group
Please refer to [how to create docker group](https://docs.docker.com/engine/installation/linux/ubuntulinux/#create-a-docker-group) for more information.
<p>Create the docker group
<br>`$ sudo groupadd docker`

Add your user to docker group.
<br>`$ sudo usermod -aG docker ubuntu`

Verify your work by running docker without sudo.
<br>`$ docker run hello-world`

If this fails with a message similar to this:

`Cannot connect to the Docker daemon. Is 'docker daemon' running on this host?`
<p>Check that the DOCKER_HOST environment variable is not set for your shell. If it is, unset it.

###Transfer of files
`$ scp <file.tar> ubuntu@12.34.56.78<Your IP Address>:12.34.89.10<Destination>`

##Build your own images

List images on host
`$ docker images`

Getting a new image
`$ docker pull ubuntu`

Pulling images
`$ docker pull docker-xeyes`

Run images in container
```
$ docker run -it docker-xeyes-container /bin/bash
root@a4cb7ce01d86:/#
```

Creating images

```
# Create a directory
$ mkdir docker-xeyes

# Create a dockerfile
$ touch dockerfile

# Open the dockerfile
$ gedit dockerfile

# Each instructions creates a new layer of the image.
FROM ubuntu:14.04
RUN apt-get update 
RUN apt-get upgrade -y
RUN apt-get install -y x11-apps

CMD xeyes

# Build the dockerfile
$ docker build -t docker-xeyes-container

# Create a .sh file
$ gedit ./run-with-x11.sh

# Type the following into .sh file
docker run -t --rm \
  -e DISPLAY=$DISPLAY \
  -u $(id -u) \
  -v /tmp/.x11-unix:/tmp/.x11-unix \
  "$@" docker-xeyes-container /bin/bash

# Run container from image
$ sudo chmod a+x ./run-with-x11.sh; ./run-with-x11.sh
```

<b>Note:</b>

The -t flag is used identify the new image belonging to docker-xeyes-container.
The location of the dockerfile using the . to indicate a Dockerfile in the current directory. <-- Can specify a path to a Dockerfile

An image can’t have more than 127 layers regardless of the storage driver. This limitation is set globally to encourage optimization of the overall size of images.

Please refer to [best practice guide for dockerfile](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/).

###ssh client display ssh server GUI

Install XRDP Package from Ubuntu Repository
`$ sudo apt-get install xrdp`

Installing the xfce4 Desktop environment
```
sudo apt-get update
sudo apt-get install xfce4
```

Configure xrdp to use xfce desktop environment
`echo xfce4-session >~/.xsession`
Restart the xrdp service
`$ sudo service xrdp restart`

Test your xrdp connection
`$ hostname -I`

Go to Windows machine and start remote desktop client and enter ip address/name of ubuntu machine.

##Q&A
-----------------
<b>Q: How do I change my permission at current folders and its sub-folder?</b>  
<p>A: Open the terminal. Go to your current folder and enter `$sudo chmod -R a+w ./`  

<b>Q: Error: Cannot connect to the Docker daemon. Is the docker daemon running on this host?</b>      
<p>A: Add sudo in front of nvidia-docker
   <p>Wrong: "nvidia-docker"
   <p>Correct: "sudo nvidia-docker"

<b>Q: How do I install caffe dependencies in c3d? </b>  
<p>A:
```
# If can't update, check proxy setting as shown above  
$ sudo apt-get update

# Install the library dependencies
$ sudo apt-get --assume-yes install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler; sudo apt-get --assume-yes install --no-install-recommends libboost-all-dev; sudo apt-get --assume-yes install libatlas-base-dev; sudo apt-get --assume-yes install libgflags-dev libgoogle-glog-dev liblmdb-dev 
```
<b>Q: How do I solve error == cudaSuccess (8 vs. 0)  invalid device function?</b>     
<p>A: Edit docker4c3d\C3D-master\Makefile.config    
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

<b>Q:How do I enable remote GUI access from windows rdp to ubuntu machine?</b>     
<br>A: ref http://c-nergy.be/blog/?p=5874   
```
$ sudo apt-get update  
$ sudo apt-get install xrdp  
$ sudo apt-get install lxde  
$ echo lxsession -s LXDE -e LXDE > ~/.xsession 
use win7 remote desktop to connect ubuntu's IP  
```

<b>Q: `# sudo apt-get update` fail behind proxy, work without proxy, why?</b>       
<br>A: Set proxy when start a container `$ docker run --env http_proxy="http://1.2.3.4:5678"`   
edit /etc/default/docker; then `$ sudo service docker restart`<- this method not effecive current system I tested

<b>Q: How do I attach to a running container?</b>       
<br>A:
```
$ sudo nvidia-docker attach container-name  <-if error "cannot attach stopped container, start it first", refer below  
$ sudo nvidia-docker start container-name  
$ sudo attach docker-attach container-name  
```

<b>Q: How do I check the version of ubuntu & docker-engine?</b>       
<br>A:
```
$ cat /etc/issue  
$ sudo docker version
```

<b>Q: How do I share files between docker container, docker host and windows PC?</b>       
<br>A: map container folder to host folder, read/write between win7 and host-folder using winscp  
ref https://winscp.net/eng/docs/guide_install

<b>Q: How do I solve this error?</b> 
<br>Error: listen tcp 127.0.0.1:3476: bind: address already in use    
A: 
```
$ ps aux | grep nvidia-docker-plugin

Display
root     xxxxx  0.0  0.0  75368  4004 pts/32   S+   11:44   0:00 sudo nvidia-docker-plugin
$ sudo kill xxxxx

# To check if the program is still running
$ ps aux | grep nvidia-docker-plugin
```
<b>Q: My IP address is not showing. How do I find my IP address?</b> 
<br>A: 
```
$ sudo ipconfig eth0 down
$ sudo ipconfig eth0 up
```

<b>Q: What is the cuda version in current container?</b>  
<br>A: execute command below  
`\# ls -all /usr/local/cuda`

<b>Q: How to run X window in container?</b>
<br>A: to check  

<b>Q: Can a container get libraries from 2 docker images? example, image1 provides cudnn4, image2 provides geany?</b>
<br>A: 

<b>Q: How to access symbolic linked file in host's folder (mapped to docker)?</b>  
<br>A: symbolic link in host-folder (mapped to container) is visible to container  

<b>Q: How I solve the following error?
<br>docker: Error while pulling image: Get https://index.docker.io/v1/repositories/library/hello-world/images: dial tcp: lookup index.docker.io on 127.0.1.1:53: no such host.</b>
<br>A: `$ nano /etc/apt/apt.conf`
<br>   `$ Acquire::http_proxy="http://1.2.3.4:5678/";`
<br>    Press Ctrl X, followed by Y and then enter.


---------------

