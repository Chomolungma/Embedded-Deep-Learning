To set Frequency for Titan X,

> For Linux PC, please add sudo in front of each command. 

```
# Enable persistence mode
nvidia-smi -pm 1

# Disable default auto boost policy
nvidia-smi --auto-boost-default=0

# List the available clocks
nvidia-smi -q -i 0 -d SUPPORTED_CLOCKS

# Set application clocks to max Memory/Graphics pair
nvidia-smi -i 0 -ac 3505,1392

# Run nvidia-smi continuously
nvidia-smi -l 

# Display Memory Utilization ratio
sudo nvidia-smi -l -i 0 -q -d UTILIZATION
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
