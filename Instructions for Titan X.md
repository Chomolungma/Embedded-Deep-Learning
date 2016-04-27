To set Frequency,

> For Linux PC, please add sudo in front of each command. 

```
#1 Enable persistence mode (Available in Linux only)
   $ nvidia-smi -pm 1

#2 By default, the auto boost under clock policy is turned on.
   To disable default auto boost policy
   $ nvidia-smi --auto-boost-default=0

#3 List the available clocks
   $ nvidia-smi -q -i 0 -d SUPPORTED_CLOCKS

#4 Set application clocks to max Memory/Graphics pair
   $ nvidia-smi -i 0 -ac 3505,1392                  <--- from step #3, get 3505 memory frequency, 1392 GPU freq
```
To run nvidia-smi
```
#5 Change Directory
   $ cd /home/ubuntu/Programs/caffe-caffe-0.14 

#6 Make a directory in caffe-caffe-0.14 to save log
   $ mkdir log

#7 To run nvidia-smi continuously at an interval of 5 secs (Default) / 1 ms
   $ nvidia-smi -l  / $ nvidia-smi --loop-ms=1
   
#8 Display the following information in a textfile (Timestamp, Total memory, Memory used, Free memory, GPU Utilization, Memory Utilization, Current SM clocks, Current Graphics Clocks, Current Memory Clocks, User specified Graphics (shader) Clocks and User specified Memory Clocks) *
   $ nvidia-smi -i 0 --loop-ms=1 --format=csv --query-gpu=timestamp,memory.total,memory.used,memory.free,utilization.gpu,utilization.memory,clocks.sm,clocks.gr,clocks.mem,clocks.applications.gr,clocks.applications.mem > nvidia-smi.txt

* Refer to https://github.com/charlyng/Embedded-Deep-Learning/blob/master/nvidia-smi-query.log to query other properties. 

#9 Run the prototxt file for AlexNet, GoogLeNet and Vgg16 **

   AlexNet
   $ LD_LIBRARY_PATH=~/Programs/opencv-2.4.10.1/build/lib ./build/tools/caffe time -model models/bvlc_alexnet/deploy1.prototxt -gpu 0 -iterations 100
   
   GoogLeNet
   $ LD_LIBRARY_PATH=~/Programs/opencv-2.4.10.1/build/lib ./build/tools/caffe time -model models/bvlc_googlenet/deploy1.prototxt -gpu 0 -iterations 100
   
   Vgg16
   $ LD_LIBRARY_PATH=~/Programs/opencv-2.4.10.1/build/lib ./build/tools/caffe time -model models/vgg16/deploy.1.prototxt -gpu 0 -iterations 100
   
   ** Make the necessary changes for different batch size to the above commands when reproducing benchmark results
   Note: deployx where x refers the batch no.  
         --> For AlexNet & GoogLeNet, deployx
         --> For Vgg16, deploy.x
  ```
