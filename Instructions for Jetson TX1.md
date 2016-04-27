To set Frequency,

> For Linux PC, please add sudo in front of each command. 

```
#1 Change Directory
   $ cd /home/ubuntu/Programs/caffe-experimental-fp16/01-tx1-settting/

#2 Change the frequency in tegra-analysis.sh *
   $ ./tegra-analysis.sh 

* Frequency will be reset after session ended. <-- mean after reboot, freq back to default value
```
To run tegrastats
```
#3 Run tegrastats
   $ ./tegrastats
```
To run protxt file
```
#4 Change Directory
   $ cd /home/ubuntu/Programs/caffe-experimental-fp16/
  
FP32

#5 Run the prototxt file for AlexNet, GoogLeNet and Vgg16 *
   AlexNet
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/bvlc_alexnet/deploy1.prototxt -gpu 0 --iterations 100
   
   GoogLeNet
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/bvlc_googlenet/deploy1.prototxt -gpu 0 --iterations 100
   
   Vgg16
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/vgg16/deploy.1.prototxt -gpu 0 --iterations 100
  
FP16

#6 Run the prototxt file for AlexNet, GoogLeNet and Vgg16 *
   AlexNet
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib ./build/tools/caffe_fp16 time -model=models/bvlc_alexnet/deploy1.prototxt -gpu 0 --iterations 100
   
   GoogLeNet
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib ./build/tools/caffe_fp16 time -model=models/bvlc_googlenet/deploy1.prototxt -gpu 0 --iterations 100
   
   Vgg16
   $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib ./build/tools/caffe_fp16 time -model=models/vgg16/deploy.1.prototxt -gpu 0 --iterations 100

   * Make the necessary changes for different batch size to the above commands when reproducing benchmark results
   Note: deployx where x refers the batch no.  
         --> For AlexNet & GoogLeNet, deployx
         --> For Vgg16, deploy.x
```
