Nvidia Benchmarking
====================

Simple benchmarking of public open-source implementations of caffe. A summary is provided in the section below.

Machine: 6-core Intel Xeon E5-2620 v3 CPU @ 2.4GHz + NVIDIA GeForce GTX Titan X + Ubuntu 14.04.03 LTS

Jetson: Nvidia Tegra X1 + Ubuntu 14.04.1 LTS

I took reference from <a href="https://www.nvidia.com/content/tegra/embedded-systems/pdf/jetson_tx1_whitepaper.pdf">Nvidia Jetson TX1 Whitepaper</a> and extracted the source from <a href="https://github.com/NVIDIA/caffe/tree/caffe-0.14"> *2 NVIDIA/caffe/tree/caffe-0.14</a> for Titan X and <a href="https://github.com/NVIDIA/caffe/tree/experimental/fp16"> *1 NVIDIA/caffe/tree/experimental/fp16</a> for Jetson TX1. 

In the following codes, I have edited <a href="https://github.com/charlyng/Embedded-Deep-Learning/blob/master/caffe.cpp">charlyng/Embedded-Deep-Learning/caffe.cpp</a> to disable the full backward pass and clock the time for a full forward pass only for 100 iterations. 

Next, I set Jetson TX1 and Titan X to a fixed frequency (Refer to <a href="https://github.com/charlyng/Embedded-Deep-Learning/blob/master/Set%20Frequency.md">charlyng/Embedded-Deep-Learning/Set Frequency.md</a>). Thereafter, I run caffe time on AlexNet, GoogLeNet and Vgg16 on Jetson TX1 (FP32), caffe_fp16 time on Jetson TX1 (FP16) and caffe time on Titan X (FP32) for Batch 1, 64 and 128 (Refer to commands in cmd_AlexNet.md, cmd_GoogLeNet.md, cmd_Vgg16.md).

**AlexNet**

<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: <br>AlexNet Batch 1</th>
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
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (fps)</td>
    <td class="tg-h0x1">45.7</td>
    <td class="tg-s6z2">65.1</td>
    <td class="tg-h0x1">408.2</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1">1372</td>
    <td class="tg-s6z2">930</td>
    <td class="tg-h0x1">519</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1">97%</td>
    <td class="tg-s6z2">32%</td>
    <td class="tg-h0x1">93%</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1">691</td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1">1202</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
</table>

<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: <br>AlexNet Batch 64</th>
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
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (fps)</td>
    <td class="tg-h0x1">127.7</td>
    <td class="tg-s6z2">253.1</td>
    <td class="tg-h0x1">2730.4</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1">2679</td>
    <td class="tg-s6z2">972</td>
    <td class="tg-h0x1">1337</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">99%</td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1">691</td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1">1202</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
</table>

<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: <br>AlexNet Batch 128</th>
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
    <td class="tg-h0x1">40.2</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (fps)</td>
    <td class="tg-h0x1">153.4</td>
    <td class="tg-s6z2">257.8</td>
    <td class="tg-h0x1">3181.7</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1">2886</td>
    <td class="tg-s6z2">1146</td>
    <td class="tg-h0x1">1804</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">99%</td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1">691</td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1">1202</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
</table>

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

**GoogLeNet**

<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: <br>GoogLeNet Batch 1</th>
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
    <td class="tg-h0x1">29.3</td>
    <td class="tg-s6z2">23.7</td>
    <td class="tg-h0x1">7.6</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (fps)</td>
    <td class="tg-h0x1">34.2</td>
    <td class="tg-s6z2">42.1</td>
    <td class="tg-h0x1">131.1</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1">1274</td>
    <td class="tg-s6z2">950</td>
    <td class="tg-h0x1">519</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1">97%</td>
    <td class="tg-s6z2">99%</td>
    <td class="tg-h0x1">93%</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1">691</td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1">1202</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
</table>

<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: <br>GoogLeNet Batch 64</th>
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
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2">839.2</td>
    <td class="tg-h0x1">68.7</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (fps)</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2">76.3</td>
    <td class="tg-h0x1">931</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2">1726</td>
    <td class="tg-h0x1">3163</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2">99%</td>
    <td class="tg-h0x1">98%</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1">691</td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1">1202</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
</table>

<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: <br>GoogLeNet Batch 128</th>
    <th class="tg-hgcj" colspan="3">cuDNN4</th>
    <th class="tg-hgcj" colspan="3">cuDNN 5</th>
  </tr>
    <td class="tg-aa40">Tegra X1 *1<br>(FP32)</td>
    <td class="tg-hgcj">Tegra X1 *1<br>(FP16)</td>
    <td class="tg-aa40">Titan X *2<br>(FP32)</td>
    <td class="tg-hgcj">Tegra X1 *1<br>(FP32)</td>
    <td class="tg-aa40">Tegra X1 *1<br>(FP16)</td>
    <td class="tg-hgcj">Titan X *2<br>(FP32)</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (ms)</td>
    <td class="tg-h0x1">N.A</td>
    <td class="tg-s6z2">1672.3</td>
    <td class="tg-h0x1">130.8</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (fps)</td>
    <td class="tg-h0x1">N.A</td>
    <td class="tg-s6z2">76.5</td>
    <td class="tg-h0x1">978.4</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1">N.A</td>
    <td class="tg-s6z2">3387</td>
    <td class="tg-h0x1">5522</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1">N.A</td>
    <td class="tg-s6z2">99%</td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1">N.A</td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1">1202</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
</table>

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Vgg16**

<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: <br>Vgg16 Batch 1</th>
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
    <td class="tg-h0x1">156.1</td>
    <td class="tg-s6z2">104.4</td>
    <td class="tg-h0x1">12</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (fps)</td>
    <td class="tg-h0x1">6.4</td>
    <td class="tg-s6z2">9.6</td>
    <td class="tg-h0x1">83.5</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1">2019</td>
    <td class="tg-s6z2">1154</td>
    <td class="tg-h0x1">5522</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">99%</td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1">691</td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1">1202</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
</table>

</style>
<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: <br>Vgg16 Batch 64</th>
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
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2">5150.6</td>
    <td class="tg-h0x1">307.6</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (fps)</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2">12.4</td>
    <td class="tg-h0x1">208.1</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2">2971</td>
    <td class="tg-h0x1">9973</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2">99%</td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2">691</td>
    <td class="tg-h0x1">1202</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
</table>

<table class="tg">
  <tr>
    <th class="tg-hgcj" rowspan="2">Network: <br>Vgg16 Batch 128</th>
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
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1">604.8</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Average Forward Pass (fps)</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1">211.6</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-031e">Memory (MBytes)</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1">12287</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Utilization Average</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1">99%</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
  <tr>
    <td class="tg-yw4l">GPU Frequency (MHz)</td>
    <td class="tg-h0x1"></td>
    <td class="tg-s6z2"></td>
    <td class="tg-h0x1">1202</td>
    <td class="tg-s6z2">TBC</td>
    <td class="tg-h0x1">TBC</td>
    <td class="tg-s6z2">TBC</td>
  </tr>
</table>
