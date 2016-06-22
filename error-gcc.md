error: libdc1394 error: Failed to initialize libdc1394
solution: sudo ln /dev/null /dev/raw1394 
verified in docker container, ref https://github.com/jsk-ros-pkg/jsk_travis/issues/187
