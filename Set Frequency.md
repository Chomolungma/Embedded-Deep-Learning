To set Frequency for Titan X,

```
# Enable persistence mode
sudo nvidia-smi -pm 1

# Disable default auto boost policy
sudo nvidia-smi --auto-boost-default=0

# Set application clocks to 1392MHz to 3505MHz
sudo nvidia-smi -i 0 -ac 3505,1392

# Run nvidia-smi continuously
sudo nvidia-smi -l 
```
Frequency will be reset after session ended.

To set Frequency for Jetson TX1,

```
# Change directory to 01-tx1-settting
cd /home/ubuntu/Programs/caffe-experimental-fp16/01-tx1-settting/

# Change the frequency in tegra-analysis.sh
sudo ./tegra-analysis.sh

# Run tegrastats
sudo ./tegrastats
```
