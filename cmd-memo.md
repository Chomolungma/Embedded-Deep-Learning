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
