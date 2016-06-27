# Benchmarking of Caffe on Jetson TX1

<b>Change Frequency Settings</b>

> For Linux PC, please add sudo in front of each command. 

```
#1 Change Directory
   $ cd /home/ubuntu/Programs/caffe-experimental-fp16/01-tx1-settting/
   
#2 Replace tegra-analysis.sh with paper-tegra-analysis-690M.sh
   Src: https://github.com/charlyng/Embedded-Deep-Learning/tree/fcc8b7e13dcfc5767da277700caf6a67e19a91b0/tx1-freq-settting

#3 Change the frequency in tegra-analysis.sh *
   $ ./paper-tegra-analysis-690M.sh 

* Frequency will be reset after session ended. <-- mean after reboot, freq back to default value
```
<b>Run tegrastats</b>
```
#4 Run tegrastats
   $ ./tegrastats
```
<b>Run prototxt file</b>
```
#5 Change Directory
   $ cd /home/ubuntu/Programs/caffe-experimental-fp16/
  
FP32

#6 Run the prototxt file for AlexNet, GoogLeNet and Vgg16 *
   AlexNet
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/bvlc_alexnet/deploy1.prototxt -gpu 0 --iterations 100
   
   GoogLeNet
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/bvlc_googlenet/deploy1.prototxt -gpu 0 --iterations 100
   
   Vgg16
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/vgg16/deploy.1.prototxt -gpu 0 --iterations 100
  
FP16

#7 Run the prototxt file for AlexNet, GoogLeNet and Vgg16 *
   AlexNet
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe_fp16 time -model=models/bvlc_alexnet/deploy1.prototxt -gpu 0 --iterations 100
   
   GoogLeNet
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe_fp16 time -model=models/bvlc_googlenet/deploy1.prototxt -gpu 0 --iterations 100
   
   Vgg16
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe_fp16 time -model=models/vgg16/deploy.1.prototxt -gpu 0 --iterations 100

   * Make the necessary changes for different batch size to the above commands when reproducing benchmark results
   Note: deployx where x refers the batch no.  
         --> For AlexNet & GoogLeNet, deployx
         --> For Vgg16, deploy.x
```
