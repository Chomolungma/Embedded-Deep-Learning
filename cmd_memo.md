 You can also debug included headers and check that there is no mix of 2.4/3.1 headers [src https://github.com/Itseez/opencv/issues/6076]
g++ -E -x c++ - -v `pkg-config opencv --cflags --libs` <<< '#include "opencv2/opencv.hpp"' | grep  "# 1 .*opencv2.*1"
