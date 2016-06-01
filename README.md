Nvidia Benchmarking
====================

Simple benchmarking of public open-source implementations of caffe. A summary is provided in the section below.

Machine: 6-core Intel Xeon E5-2620 v3 CPU @ 2.4GHz + NVIDIA GeForce GTX Titan X + Ubuntu 14.04.03 LTS

Jetson: Nvidia Tegra X1 + Ubuntu 14.04.1 LTS

I took reference from <a href="https://www.nvidia.com/content/tegra/embedded-systems/pdf/jetson_tx1_whitepaper.pdf">Nvidia Jetson TX1 Whitepaper</a> and extracted the source from <a href="https://github.com/NVIDIA/caffe/tree/caffe-0.14"> [2] NVIDIA/caffe/tree/caffe-0.14</a> for Titan X and <a href="https://github.com/NVIDIA/caffe/tree/experimental/fp16"> [1] NVIDIA/caffe/tree/experimental/fp16</a> for Jetson TX1. 

In the following codes, I have edited <a href="https://github.com/charlyng/Embedded-Deep-Learning/blob/master/caffe.cpp">charlyng/Embedded-Deep-Learning/caffe.cpp</a> to disable the full backward pass and clock the time for a full forward pass only for 100 iterations. 

Next, I set Jetson TX1 and Titan X to a fixed frequency (Refer to <a href="https://github.com/charlyng/Embedded-Deep-Learning/blob/master/Set%20Frequency.md">charlyng/Embedded-Deep-Learning/Set Frequency.md</a>). Thereafter, I run caffe time on AlexNet, GoogLeNet and Vgg16 on Jetson TX1 (FP32), caffe_fp16 time on Jetson TX1 (FP16) and caffe time on Titan X (FP32) for Batch 1, 64 and 128 (Refer to commands in cmd_AlexNet.md, cmd_GoogLeNet.md, cmd_Vgg16.md).

**AlexNet**


<table>
  <tr>
    <th rowspan="2">Network: AlexNet</th>
    <th rowspan="2">Batch<br>Size</th>
    <th colspan="3">cuDNN4</th>
    <th colspan="3">cuDNN5</th>
  </tr>
  <tr>
    <td>Tegra X1<br>(FP32)</td>
    <td>Tegra X1<br>(FP16)</td>
    <td>Titan X<br>(FP32)</td>
    <td>Tegra X1<br>(FP32)</td>
    <td>Tegra X1<br>(FP16)</td>
    <td>Titan X<br>(FP32)</td>
  </tr>
  <tr>
    <td>Average Forward Pass (ms)</td>
    <td rowspan="5">1</td>
    <td>21.9</td>
    <td>15.4</td>
    <td>2.5</td>
    <td colspan="3" rowspan="5">TBC</td>
  </tr>
  <tr>
    <td>Average Forward Pass (fps)</td>
    <td>45.7</td>
    <td>65.1</td>
    <td>408.2</td>
  </tr>
  <tr>
    <td>Memory (Mbytes)</td>
    <td>1372</td>
    <td>930</td>
    <td>519</td>
  </tr>
  <tr>
    <td>GPU Utilization Average</td>
    <td>97%</td>
    <td>32%</td>
    <td>93%</td>
  </tr>
  <tr>
    <td>GPU Frequency (MHz)</td>
    <td>691</td>
    <td>691</td>
    <td>1202</td>
  </tr>
  <tr>
    <td>Average Forward Pass (ms)</td>
    <td rowspan="5">64</td>
    <td>501.2</td>
    <td>252.8</td>
    <td>23.4</td>
    <td colspan="3" rowspan="5">TBC</td>
  </tr>
  <tr>
    <td>Average Forward Pass (fps)</td>
    <td>127.7</td>
    <td>253.1</td>
    <td>2730.4</td>
  </tr>
  <tr>
    <td>Memory (Mbytes)</td>
    <td>2679</td>
    <td>972</td>
    <td>1337</td>
  </tr>
  <tr>
    <td>GPU Utilization Average</td>
    <td>99%</td>
    <td>99%</td>
    <td>99%</td>
  </tr>
  <tr>
    <td>GPU Frequency (MHz)</td>
    <td>691</td>
    <td>691</td>
    <td>1202</td>
  </tr>
  <tr>
    <td>Average Forward Pass (ms)</td>
    <td rowspan="5">128</td>
    <td>834.2</td>
    <td>496.6</td>
    <td>40.2</td>
    <td colspan="3" rowspan="5">TBC</td>
  </tr>
  <tr>
    <td>Average Forward Pass (fps)</td>
    <td>153.4</td>
    <td>257.8</td>
    <td>3181.7</td>
  </tr>
  <tr>
    <td>Memory (Mbytes)</td>
    <td>2886</td>
    <td>1146</td>
    <td>1804</td>
  </tr>
  <tr>
    <td>GPU Utilization Average</td>
    <td>99%</td>
    <td>99%</td>
    <td>99%</td>
  </tr>
  <tr>
    <td>GPU Frequency (MHz)</td>
    <td>691</td>
    <td>691</td>
    <td>1202</td>
  </tr>
</table>

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

**GoogLeNet**

<table>
  <tr>
    <th rowspan="2">Network: GoogLeNet</th>
    <th rowspan="2">Batch<br>Size</th>
    <th colspan="3">cuDNN4</th>
    <th colspan="3">cuDNN5</th>
  </tr>
  <tr>
    <td>Tegra X1<br>(FP32)</td>
    <td>Tegra X1<br>(FP16)</td>
    <td>Titan X<br>(FP32)</td>
    <td>Tegra X1<br>(FP32)</td>
    <td>Tegra X1<br>(FP16)</td>
    <td>Titan X<br>(FP32)</td>
  </tr>
  <tr>
    <td>Average Forward Pass (ms)</td>
    <td rowspan="5">1</td>
    <td>29.3</td>
    <td>23.7</td>
    <td>7.6</td>
    <td colspan="3" rowspan="5">TBC</td>
  </tr>
  <tr>
    <td>Average Forward Pass (fps)</td>
    <td>34.2</td>
    <td>42.1</td>
    <td>131.1</td>
  </tr>
  <tr>
    <td>Memory (Mbytes)</td>
    <td>1274</td>
    <td>950</td>
    <td>519</td>
  </tr>
  <tr>
    <td>GPU Utilization Average</td>
    <td>97%</td>
    <td>99%</td>
    <td>93%</td>
  </tr>
  <tr>
    <td>GPU Frequency (MHz)</td>
    <td>691</td>
    <td>691</td>
    <td>1202</td>
  </tr>
  <tr>
    <td>Average Forward Pass (ms)</td>
    <td rowspan="5">64</td>
    <td>NA</td>
    <td>839.2</td>
    <td>68.7</td>
    <td colspan="3" rowspan="5">TBC</td>
  </tr>
  <tr>
    <td>Average Forward Pass (fps)</td>
    <td>NA</td>
    <td>76.3</td>
    <td>931</td>
  </tr>
  <tr>
    <td>Memory (Mbytes)</td>
    <td>NA</td>
    <td>1726</td>
    <td>3163</td>
  </tr>
  <tr>
    <td>GPU Utilization Average</td>
    <td>NA</td>
    <td>99%</td>
    <td>98%</td>
  </tr>
  <tr>
    <td>GPU Frequency (MHz)</td>
    <td>NA</td>
    <td>691</td>
    <td>1202</td>
  </tr>
  <tr>
    <td>Average Forward Pass (ms)</td>
    <td rowspan="5">128</td>
    <td>NA</td>
    <td>1672.3</td>
    <td>130.8</td>
    <td colspan="3" rowspan="5">TBC</td>
  </tr>
  <tr>
    <td>Average Forward Pass (fps)</td>
    <td>NA</td>
    <td>76.5</td>
    <td>978.4</td>
  </tr>
  <tr>
    <td>Memory (Mbytes)</td>
    <td>NA</td>
    <td>3387</td>
    <td>5522</td>
  </tr>
  <tr>
    <td>GPU Utilization Average</td>
    <td>NA</td>
    <td>99%</td>
    <td>99%</td>
  </tr>
  <tr>
    <td>GPU Frequency (MHz)</td>
    <td>NA</td>
    <td>691</td>
    <td>1202</td>
  </tr>
</table>

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Vgg16**

<table>
  <tr>
    <th rowspan="2">Network: Vgg16</th>
    <th rowspan="2">Batch<br>Size</th>
    <th colspan="3">cuDNN4</th>
    <th colspan="3">cuDNN5</th>
  </tr>
  <tr>
    <td>Tegra X1<br>(FP32)</td>
    <td>Tegra X1<br>(FP16)</td>
    <td>Titan X<br>(FP32)</td>
    <td>Tegra X1<br>(FP32)</td>
    <td>Tegra X1<br>(FP16)</td>
    <td>Titan X<br>(FP32)</td>
  </tr>
  <tr>
    <td>Average Forward Pass (ms)</td>
    <td rowspan="5">1</td>
    <td>156.1</td>
    <td>104.4</td>
    <td>12</td>
    <td colspan="3" rowspan="5">TBC</td>
  </tr>
  <tr>
    <td>Average Forward Pass (fps)</td>
    <td>6.4</td>
    <td>9.6</td>
    <td>83.5</td>
  </tr>
  <tr>
    <td>Memory (Mbytes)</td>
    <td>2019</td>
    <td>1154</td>
    <td>5522</td>
  </tr>
  <tr>
    <td>GPU Utilization Average</td>
    <td>99%</td>
    <td>99%</td>
    <td>99%</td>
  </tr>
  <tr>
    <td>GPU Frequency (MHz)</td>
    <td>691</td>
    <td>691</td>
    <td>1202</td>
  </tr>
  <tr>
    <td>Average Forward Pass (ms)</td>
    <td rowspan="5">64</td>
    <td>NA</td>
    <td>5150.6</td>
    <td>307.6</td>
    <td colspan="3" rowspan="5">TBC</td>
  </tr>
  <tr>
    <td>Average Forward Pass (fps)</td>
    <td>NA</td>
    <td>12.4</td>
    <td>208.1</td>
  </tr>
  <tr>
    <td>Memory (Mbytes)</td>
    <td>NA</td>
    <td>2971</td>
    <td>9973</td>
  </tr>
  <tr>
    <td>GPU Utilization Average</td>
    <td>NA</td>
    <td>99%</td>
    <td>99%</td>
  </tr>
  <tr>
    <td>GPU Frequency (MHz)</td>
    <td>NA</td>
    <td>691</td>
    <td>1202</td>
  </tr>
  <tr>
    <td>Average Forward Pass (ms)</td>
    <td rowspan="5">128</td>
    <td>NA</td>
    <td>NA</td>
    <td>604.8</td>
    <td colspan="3" rowspan="5">TBC</td>
  </tr>
  <tr>
    <td>Average Forward Pass (fps)</td>
    <td>NA</td>
    <td>NA</td>
    <td>211.6</td>
  </tr>
  <tr>
    <td>Memory (Mbytes)</td>
    <td>NA</td>
    <td>NA</td>
    <td>12287</td>
  </tr>
  <tr>
    <td>GPU Utilization Average</td>
    <td>NA</td>
    <td>NA</td>
    <td>99%</td>
  </tr>
  <tr>
    <td>GPU Frequency (MHz)</td>
    <td>NA</td>
    <td>NA</td>
    <td>1202</td>
  </tr>
</table>
