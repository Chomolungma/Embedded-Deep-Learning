Troubleshooting
---------------

<b>Darket (yolo)</b>

Command: git clone https://github.com/pjreddie/darknet.git

Error Message: Error "fatal: unable to access 'https://github.com/pjreddie/darknet.git/': Could not resolve proxy: proxy"

Solution: `$ unset http_proxy; unset https_proxy`

<b>OpenCV</b>

Check that there is no mix of 2.4/3.2 headers [Src: https://github.com/Itseez/opencv/issues/6076]
```
g++ -E -x c++ - -v `pkg-config opencv --cflags --libs` <<< '#include "opencv2/opencv.hpp"' | grep  "# 1 .*opencv2.*1"
```

```
$ pkg-config --cflags --libs opencv

$ pkg-config --modversion opencv

$ make uninstall
```

<b> zip / unzip </b>
$tar -czvf test.tar.gz test <- preserve symbolic links
$tar -xhzvf test.tar.gz <-use "-h" argument to save the symlink

###windows comamnd
####create virtual drive
ref https://technet.microsoft.com/ja-jp/library/bb491006.aspx
ref http://www.ntwind.com/software/utilities/visual-subst.html

start windows comamnd prompt as admin, 
>cd n:      <- check N drive exist?  
>subst N: C:\Users\avc2\Downloads\weisheng\N-drive  
>cd n:      <- check created  

####delete virtual drive
>cd n:     <- check exist  
>subst N: /d <- delete  
>cd n:     <- check created  

mount thumbdrive as ubuntu folder
http://askubuntu.com/questions/37767/how-to-access-a-usb-flash-drive-from-the-terminal-how-can-i-mount-a-flash-driv
You'll need to know what the drive is called to mount it. To do that fire off:

sudo fdisk -l

You're looking for a partition that should look something like: /dev/sdb1. Remember what it's called.
2. Create a mount point

Create a new directory in /media so you can mount the drive onto the filesystem:

sudo  mkdir /media/usb

3. Mount!

sudo mount /dev/sdb1 /media/usb

When you're done, just fire off:

sudo umount /media/usb


$ sudo mkdir /media/usb1
$ sudo mount -t ntfs-3g /dev/sda1 /media/usb1
$ sudo chmod -R 777 /media/usb1

compress by preserving symbolic links in a folder (don't zip destination of symbolic link to reduce filesize)  
zip -ry output-file.zip /source/folder/that/include/symbolic-link  

scp through tunnel
local_L -> tunnel_T -> desti_T  
file_T <---------------- file_T  
Run scp to machine R, which is only accessible through gateway machine G    

mobilexterm local terminal window1  
ssh -L 1234:desti_T_IP:22 tunne_T_user@tunnel_T_IP  

mobilexterm local terminal window1  
scp -P 1234 ubuntu@127.0.0.1:/desti_T_path/file_T /local_L_patth/file_T  

replace string from all found files from "/s" to "/g"  
 find ./ -type f -name "*.cu" -exec sed -i 's/__UNIX__/__unix__/g' {} +  

