AlexNet Batch 1
---------------
<b>Jetson TX1 (FP32)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/bvlc_alexnet/deploy1.prototxt -gpu 0 --iterations 100`

<b>Jetson TX1 (FP16)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib ./build/tools/caffe_fp16 time -model=models/bvlc_alexnet/deploy1.prototxt -gpu 0 --iterations 100`

<b>Titanx X (FP32)</b>

`LD_LIBRARY_PATH=~/Programs/opencv-2.4.10.1/build/lib ./build/tools/caffe time -model models/bvlc_alexnet/deploy.1.prototxt -gpu 0 -iterations 100`

AlexNet Batch 64
----------------
<b>Jetson TX1 (FP32)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/bvlc_alexnet/deploy64.prototxt -gpu 0 --iterations 100`

<b>Jetson TX1 (FP16)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib ./build/tools/caffe_fp16 time -model=models/bvlc_alexnet/deploy64.prototxt -gpu 0 --iterations 100`

<b>Titanx X (FP32)</b>

`LD_LIBRARY_PATH=~/Programs/opencv-2.4.10.1/build/lib ./build/tools/caffe time -model models/bvlc_alexnet/deploy.64.prototxt -gpu 0 -iterations 100`

AlexNet Batch 128
-----------------
<b>Jetson TX1 (FP32)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/bvlc_alexnet/deploy128.prototxt -gpu 0 --iterations 100`

<b>Jetson TX1 (FP16)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib ./build/tools/caffe_fp16 time -model=models/bvlc_alexnet/deploy128.prototxt -gpu 0 --iterations 100`

<b>Titanx X (FP32)</b>

`LD_LIBRARY_PATH=~/Programs/opencv-2.4.10.1/build/lib ./build/tools/caffe time -model models/bvlc_alexnet/deploy.128.prototxt -gpu 0 -iterations 100`
 
