Vgg16 Batch 1
---------------
<b>Jetson TX1 (FP32)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/vgg16/deploy1.prototxt -gpu 0 --iterations 100`

<b>Jetson TX1 (FP16)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib ./build/tools/caffe_fp16 time -model=models/vgg16/deploy1.prototxt -gpu 0 --iterations 100`

<b>Titanx X (FP32)</b>

`LD_LIBRARY_PATH=~/Programs/opencv-2.4.10.1/build/lib ./build/tools/caffe time -model models/vgg16/deploy.1.prototxt -gpu 0 -iterations 100`

Vgg16 Batch 64
----------------
<b>Jetson TX1 (FP32)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/vgg16/deploy64.prototxt -gpu 0 --iterations 100`

<b>Jetson TX1 (FP16)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib ./build/tools/caffe_fp16 time -model=models/vgg16/deploy64.prototxt -gpu 0 --iterations 100`

<b>Titanx X (FP32)</b>

`LD_LIBRARY_PATH=~/Programs/opencv-2.4.10.1/build/lib ./build/tools/caffe time -model models/vgg16/deploy.64.prototxt -gpu 0 -iterations 100`

Vgg16 Batch 128
-----------------
<b>Jetson TX1 (FP32)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib; ./build/tools/caffe time -model=models/vgg16/deploy128.prototxt -gpu 0 --iterations 100`

<b>Jetson TX1 (FP16)</b>

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib ./build/tools/caffe_fp16 time -model=models/vgg16/deploy128.prototxt -gpu 0 --iterations 100`

<b>Titanx X (FP32)</b>

`LD_LIBRARY_PATH=~/Programs/opencv-2.4.10.1/build/lib ./build/tools/caffe time -model models/vgg16/deploy.128.prototxt -gpu 0 -iterations 100`
