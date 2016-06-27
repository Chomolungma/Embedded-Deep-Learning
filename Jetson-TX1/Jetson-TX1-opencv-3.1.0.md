Current working Environment Setup: Jetson TX1 (L4T R23.2) + OpenCv-3.1.0 + CUDA 7.0 + USB_Cam*
* Logitech HD Pro Webcam C910 [Src: <a href="http://support.logitech.com/en_us/product/hd-pro-webcam-c910">http://support.logitech.com/en_us/product/hd-pro-webcam-c910</a>]

<b>Uninstall Current OpenCV</b>
```
# Change Directory
$ cd /usr/local/include

# Remove openCV folder
$ sudo rm -rf opencv
$ sudo rm -rf opencv2

# Change Directory
$ cd /usr/local/lib

# Remove all libopencv_ related files
$ sudo rm libopencv_*
```
<b>Install OpenCV-3.1.0 on Jetson TX1</b> [src: <a href="https://devtalk.nvidia.com/default/topic/917386/jetson-tx1/usb-3-0-port-unstable-on-jetson-tx1-/post/4835793/#4835793">Instructions to install OpenCV-3.1.0</a>]

1.  Download "OpenCV for Linux/Mac (Version 3.1)" from http://opencv.org/downloads.html

2. Compile and install OpenCV-3.1.0 by following the official Jetson Installing_OpenCV guide

    ```
    # Add universal repository to Ubuntu
   $ sudo apt-add-repository universe
   $ sudo apt-get update

   # Some general development libraries
   $ sudo apt-get install -y build-essential make cmake cmake-curses-gui g++

   # libav video input/output development libraries
   $ sudo apt-get install -y libavformat-dev libavutil-dev libswscale-dev

   # Video4Linux camera development libraries
   $ sudo apt-get install -y libv4l-dev

   # Eigen3 math development libraries
   $ sudo apt-get install -y libeigen3-dev

   # OpenGL development libraries (to allow creating graphical windows)
   $ sudo apt-get install -y libglew1.6-dev

   # GTK development libraries (to allow creating graphical windows)
   $ sudo apt-get install -y libgtk2.0-dev

   # Compile and install opencv
   $ cd ~/Programs
   $ unzip opencv-3.1.0.zip
   $ cd opencv-3.1.0
   $ mkdir build
   $ cd build
   $ cmake -DWITH_CUDA=ON -DCUDA_ARCH_BIN="5.3" -DCUDA_ARCH_PTX="" -DBUILD_TESTS=OFF -DBUILD_PERF_TESTS=OFF -DCUDA_FAST_MATH=ON  -DCMAKE_INSTALL_PREFIX=/home/ubuntu/Programs/opencv-3.1.0 ..
   $ make -j4 install
 ```
3. Compile and run the OpenCV gpu "hog" sample program with Logitech HD Pro Webcam C910 camera as the video source.

   ```
   $ cd ~/Programs/opencv-3.1.0/samples/gpu
   $ g++ -o hog -I /home/ubuntu/Programs/opencv-3.1.0/include -O2 -g -Wall hog.cpp -L /home/ubuntu/Programs/opencv-3.1.0/lib -lopencv_core -lopencv_imgproc -l opencv_flann -l opencv_imgcodecs -lopencv_videoio -lopencv_highgui -lopencv_ml -lopencv_video -lopencv_objdetect -lopencv_photo -lopencv_features2d -lopencv_calib3d -lopencv_stitching -lopencv_videostab -lopencv_shape -lopencv_cudaobjdetect -lopencv_cudawarping -lopencv_cudaimgproc
   $ export LD_LIBRARY_PATH=/home/ubuntu/Programs/opencv-3.1.0/lib:$LD_LIBRARY_PATH
   $ ./hog --camera 0
```

