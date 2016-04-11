Nvidia Benchmarking
====================

Simple benchmarking of public open-source implementations of caffe. A summary is provided in the section below.

Machine: 6-core Intel Xeon E5-2620 v3 CPU @ 2.4GHz + NVIDIA GeForce GTX Titan X + Ubuntu 14.04.03 LTS

Jetson: Nvidia Tegra X1 + Ubuntu 14.04.1 LTS

I took reference from <a href="https://www.nvidia.com/content/tegra/embedded-systems/pdf/jetson_tx1_whitepaper.pdf">Nvidia Jetson TX1 Whitepaper</a> and extracted the source from <a href="https://github.com/NVIDIA/caffe/tree/caffe-0.14"> /*2 NVIDIA/caffe/tree/caffe-0.14</a> for Titan X and <a href="https://github.com/NVIDIA/caffe/tree/experimental/fp16"> /*1 NVIDIA/caffe/tree/experimental/fp16</a> for Jetson TX1. 

In the following codes, I have edited <a href="https://github.com/charlyng/Embedded-Deep-Learning/blob/master/caffe.cpp">charlyng/Embedded-Deep-Learning/caffe.cpp</a> to disable the full backward pass and clock the time for a full forward pass only for 100 iterations. 

Next, I set Jetson TX1 and Titan X to a fixed frequency (Refer to <a href="https://github.com/charlyng/Embedded-Deep-Learning/blob/master/Set Frequency.cpp">charlyng/Embedded-Deep-Learning/Set Frequency.md</a>). Thereafter, I run caffe time on AlexNet, GoogLeNet and Vgg16 on Jetson TX1 (FP32), caffe_fp16 time on Jetson TX1 (FP16) and caffe time on Titan X (FP32) for Batch 1, 64 and 128 (Refer to commands in cmd_AlexNet.md, cmd_GoogLeNet.md, cmd_Vgg16.md).

**AlexNet**

| Network: AlexNet Batch 1     | Tegra X1 (FP32)*1 | Tegra X1 (FP16)*1 | Titan X (FP32)*2 |
| ---------------------------- |:---------------:|:---------------:|:--------------:|
| Average Forward Pass (ms)    | 21.9            | 15.4            | 2.5            |
| Average Forward Pass (fps)   | 45.7            | 65.1            | 408.2          |
| Memory (Mbytes)              | 1372            | 930             |                |
| GPU Utilization Average      | 97%             | 32%             |                |
| GPU Frequency (MHz)          | 691             | 691             |                |

| Network: AlexNet Batch 64    | Tegra X1 (FP32) | Tegra X1 (FP16) | Titan X (FP32) |
| ---------------------------- |:---------------:|:---------------:|:--------------:|
| Average Forward Pass (ms)    | 501.2           | 252.8           | 23.4           |
| Average Forward Pass (fps)   | 127.7           | 253.1           | 2732.7         |
| Memory (Mbytes)              | 2679            | 972             |                |
| GPU Utilization Average      | 99%             | 99%             |                |
| GPU Frequency (MHz)          | 691             | 691             |                |

| Network: AlexNet Batch 128   | Tegra X1 (FP32) | Tegra X1 (FP16) | Titan X (FP32) |
| ---------------------------- |:---------------:|:---------------:| :-------------:|
| Average Forward Pass (ms)    | 834.2           | 496.6           | 40.3           |
| Average Forward Pass (fps)   | 153.4           | 257.8           | 3178.5         |
| Memory (Mbytes)              | 2886            | 1146            |                |
| GPU Utilization Average      | 99%             | 99%             |                |
| GPU Frequency (MHz)          | 691             | 691             |                |

<p>---------------------------------------------------------------------------------------------------------------------------------</p>

**GoogLeNet**

| Network: GoogLeNet Batch 1   | Tegra X1 (FP32) | Tegra X1 (FP16) | Titan X (FP32) |
| ---------------------------- |:---------------:|:---------------:|:--------------:|
| Average Forward Pass (ms)    | 29.3            | 23.7            | 7.6            |
| Average Forward Pass (fps)   | 34.2            | 42.1            | 131.4          |
| Memory (Mbytes)              | 1274            | 950             |                |
| GPU Utilization Average      | 97%             | 99%             |                |
| GPU Frequency (MHz)          | 691             | 691             |                |

| Network: GoogLeNet Batch 64  | Tegra X1 (FP32) | Tegra X1 (FP16) | Titan X (FP32) |
| ---------------------------- |:---------------:|:---------------:|:--------------:|
| Average Forward Pass (ms)    |                 | 839.2           | 68.8           |
| Average Forward Pass (fps)   |                 | 76.3            | 930.9          |
| Memory (Mbytes)              |                 | 1726            |                |
| GPU Utilization Average      |                 | 99%             |                |
| GPU Frequency (MHz)          | 691             | 691             |                |

| Network: GoogLeNet Batch 128 | Tegra X1 (FP32) | Tegra X1 (FP16) | Titan X (FP32) |
| ---------------------------- |:---------------:|:---------------:|:--------------:|
| Average Forward Pass (ms)    | N.A             | 1672.3          | 131.1          |
| Average Forward Pass (fps)   | N.A             | 76.5            | 976.6          |
| Memory (Mbytes)              | N.A             | 3387            |                |
| GPU Utilization Average      | N.A             | 99%             |                |
| GPU Frequency (MHz)          | N.A             | 691             |                |

<p>---------------------------------------------------------------------------------------------------------------------------------</p>

**Vgg16**

| Network: Vgg16 Batch 1       | Tegra X1 (FP32) | Tegra X1 (FP16) | Titan X (FP32) |
| ---------------------------- |:---------------:|:---------------:|:--------------:|
| Average Forward Pass (ms)    | 156.1           | 104.4           | 12             |
| Average Forward Pass (fps)   | 6.4             | 9.6             | 83.5           |
| Memory (Mbytes)              | 2019            | 1154            |                |
| GPU Utilization Average      | 99%             | 99%             |                |
| GPU Frequency (MHz)          | 691             | 691             |                |

| Network: Vgg16 Batch 64      | Tegra X1 (FP32) | Tegra X1 (FP16) | Titan X (FP32) |
| ---------------------------- |:---------------:|:---------------:|:--------------:|
| Average Forward Pass (ms)    |                 | 5150.6          | 307.8          |
| Average Forward Pass (fps)   |                 | 12.4            | 207.9          |
| Memory (Mbytes)              |                 | 2971            |                |
| GPU Utilization Average      |                 | 99%             |                |
| GPU Frequency (MHz)          | 691             | 691             |                |

| Network: Vgg16 Batch 128     | Tegra X1 (FP32) | Tegra X1 (FP16) | Titan X (FP32) |
| ---------------------------- |:---------------:|:---------------:|:--------------:|
| Average Forward Pass (ms)    |                 |                 | 606.8          |
| Average Forward Pass (fps)   |                 |                 | 210.9          |
| Memory (Mbytes)              |                 |                 |                |
| GPU Utilization Average      |                 |                 |                |
| GPU Frequency (MHz)          | 691             | 691             |                |

