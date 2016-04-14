Nvidia Benchmarking
====================

Simple benchmarking of public open-source implementations of caffe. A summary is provided in the section below.

Machine: 6-core Intel Xeon E5-2620 v3 CPU @ 2.4GHz + NVIDIA GeForce GTX Titan X + Ubuntu 14.04.03 LTS

Jetson: Nvidia Tegra X1 + Ubuntu 14.04.1 LTS

I took reference from <a href="https://www.nvidia.com/content/tegra/embedded-systems/pdf/jetson_tx1_whitepaper.pdf">Nvidia Jetson TX1 Whitepaper</a> and extracted the source from <a href="https://github.com/NVIDIA/caffe/tree/caffe-0.14"> #2 NVIDIA/caffe/tree/caffe-0.14</a> for Titan X and <a href="https://github.com/NVIDIA/caffe/tree/experimental/fp16"> #1 NVIDIA/caffe/tree/experimental/fp16</a> for Jetson TX1. 

In the following codes, I have edited <a href="https://github.com/charlyng/Embedded-Deep-Learning/blob/master/caffe.cpp">charlyng/Embedded-Deep-Learning/caffe.cpp</a> to disable the full backward pass and clock the time for a full forward pass only for 100 iterations. 

Next, I set Jetson TX1 and Titan X to a fixed frequency (Refer to <a href="https://github.com/charlyng/Embedded-Deep-Learning/blob/master/Set%20Frequency.md">charlyng/Embedded-Deep-Learning/Set Frequency.md</a>). Thereafter, I run caffe time on AlexNet, GoogLeNet and Vgg16 on Jetson TX1 (FP32), caffe_fp16 time on Jetson TX1 (FP16) and caffe time on Titan X (FP32) for Batch 1, 64 and 128 (Refer to commands in cmd_AlexNet.md, cmd_GoogLeNet.md, cmd_Vgg16.md).

**AlexNet**

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 7px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 7px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-s6z2{text-align:center}
.tg .tg-hgcj{font-weight:bold;text-align:center}
.tg .tg-aa40{font-weight:bold;text-align:center}
.tg .tg-h0x1{text-align:center}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: AlexNet Batch 1</th>
    <th class="tg-hgcj" colspan="3">cuDNN4</th>
    <th class="tg-hgcj" colspan="3">cuDNN5</th>
  </tr>
  <tr>
    <td class="tg-aa40">Tegra X1 *1<br>(FP32)</td>
    <td class="tg-hgcj">Tegra X1 *1<br>(FP16)</td>
    <td class="tg-aa40">Titan X *2<br>(FP32)</td>
    <td class="tg-hgcj">Tegra X1 *1<br>(FP32)</td>
    <td class="tg-aa40">Tegra X1 *1<br>(FP16)</td>
    <td class="tg-hgcj">Titan X *2<br>(FP32)</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (ms)</td>
    <td class="tg-h0x1">21.9</td>
    <td class="tg-s6z2">15.4</td>
    <td class="tg-h0x1">2.5</td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forwards Pass (fps)</td>
    <td class="tg-h0x1">45.7</td>
    <td class="tg-s6z2">65.1</td>
    <td class="tg-h0x1">408.2</td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1">1372</td>
    <td class="tg-s6z2">930</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1">97%</td>
    <td class="tg-s6z2">32%</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1">691</td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
</table>

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 7px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 7px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-s6z2{text-align:center}
.tg .tg-hgcj{font-weight:bold;text-align:center}
.tg .tg-aa40{font-weight:bold;text-align:center}
.tg .tg-h0x1{text-align:center}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: AlexNet Batch 64</th>
    <th class="tg-hgcj" colspan="3">cuDNN4</th>
    <th class="tg-hgcj" colspan="3">cuDNN 5</th>
  </tr>
  <tr>
    <td class="tg-aa40">Tegra X1 *1<br>(FP32)</td>
    <td class="tg-hgcj">Tegra X1 *1<br>(FP16)</td>
    <td class="tg-aa40">Titan X *2<br>(FP32)</td>
    <td class="tg-hgcj">Tegra X1 *1<br>(FP32)</td>
    <td class="tg-aa40">Tegra X1 *1<br>(FP16)</td>
    <td class="tg-hgcj">Titan X *2<br>(FP32)</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (ms)</td>
    <td class="tg-h0x1">501.2</td>
    <td class="tg-s6z2">252.8</td>
    <td class="tg-h0x1">23.4</td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forwards Pass (fps)</td>
    <td class="tg-h0x1">127.7</td>
    <td class="tg-s6z2">253.1</td>
    <td class="tg-h0x1">2732.7</td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1">2679</td>
    <td class="tg-s6z2">972</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">99%</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1">691</td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
</table>

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 7px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 7px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-s6z2{text-align:center}
.tg .tg-hgcj{font-weight:bold;text-align:center}
.tg .tg-aa40{font-weight:bold;text-align:center}
.tg .tg-h0x1{text-align:center}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: AlexNet Batch 128</th>
    <th class="tg-hgcj" colspan="3">cuDNN4</th>
    <th class="tg-hgcj" colspan="3">cuDNN 5</th>
  </tr>
  <tr>
    <td class="tg-aa40">Tegra X1 *1<br>(FP32)</td>
    <td class="tg-hgcj">Tegra X1 *1<br>(FP16)</td>
    <td class="tg-aa40">Titan X *2<br>(FP32)</td>
    <td class="tg-hgcj">Tegra X1 *1<br>(FP32)</td>
    <td class="tg-aa40">Tegra X1 *1<br>(FP16)</td>
    <td class="tg-hgcj">Titan X *2<br>(FP32)</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (ms)</td>
    <td class="tg-h0x1">834.2</td>
    <td class="tg-s6z2">496.6</td>
    <td class="tg-h0x1">40.3</td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forwards Pass (fps)</td>
    <td class="tg-h0x1">153.4</td>
    <td class="tg-s6z2">257.8</td>
    <td class="tg-h0x1">3178.5</td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1">2886</td>
    <td class="tg-s6z2">1146</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">99%</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1">691</td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
  </tr>
</table>

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

