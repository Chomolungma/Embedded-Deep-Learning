To set Frequency for Titan X,

> For Linux PC, please add sudo in front of each command. 

```
#1 Enable persistence mode (Available in Linux only)
   nvidia-smi -pm 1

#2 By default, the auto boost under clock policy is turned on.
   To disable default auto boost policy
   nvidia-smi --auto-boost-default=0
   The auto boost under clock policy

#3 List the available clocks
nvidia-smi -q -i 0 -d SUPPORTED_CLOCKS

#4 Set application clocks to max Memory/Graphics pair
nvidia-smi -i 0 -ac 3505,1392                  <--- from step #3, get 3505 memory frequncy, 1392 GPU freq

#5 Run nvidia-smi continuously with interval of 5sec
nvidia-smi -l 

#6 Display Memory Utilization ratio
nvidia-smi -l -i 0 -q -d UTILIZATION

#7 Run the prototxt file
LD_LIBRARY_PATH=~/Programs/opencv-2.4.10.1/build/lib ./build/tools/caffe time -model models/bvlc_alexnet/deploy1.prototxt -gpu 0 -iterations 100 
```
Frequency will be reset after session ended. <-- mean after reboot, freq back to default value

To set Frequency for Jetson TX1,

```
# Change directory to 01-tx1-settting
cd /home/ubuntu/Programs/caffe-experimental-fp16/01-tx1-settting/

# Change the frequency in tegra-analysis.sh
sudo ./tegra-analysis.sh                               <--- to upload contents of this shell script

# Run tegrastats
sudo ./tegrastats
```
