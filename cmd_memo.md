 You can also debug included headers and check that there is no mix of 2.4/3.1 headers [src https://github.com/Itseez/opencv/issues/6076]

g++ -E -x c++ - -v `pkg-config opencv --cflags --libs` <<< '#include "opencv2/opencv.hpp"' | grep  "# 1 .*opencv2.*1"

`g++ -E -x c++ - -v `pkg-config opencv --cflags --libs` <<< '#include "opencv2/opencv.hpp"' | grep  "# 1 .*opencv2.*1"`

<b>Command:</b> git clone https://github.com/pjreddie/darknet.git

Error "fatal: unable to access 'https://github.com/pjreddie/darknet.git/': Could not resolve proxy: proxy"

<b>Solution:</b> unset http_proxy; unset https_proxy


pkg-config --cflags --libs opencv
pkg-config --modversion opencv
make uninstall

Uninstall opencv
cd /usr/local/include
sudo rm -rf opencv
sudo rm -rf opencv2
cd /usr/local/lib
sudo rm libopencv_*
