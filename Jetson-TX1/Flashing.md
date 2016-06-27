Installing JetPack L4T
-----------------------

Please refer to [installation of JetPack L4T](http://docs.nvidia.com/jetpack-l4t/index.html#developertools/mobile/jetpack/l4t/2.2/jetpack_l4t_install.htm) and [youtube video on JetPack installation](http://jetsonhacks.com/2015/11/18/jetpack-2-0-nvack-jetson-tx1/) for more information.

JetPack L4T requires an ubuntu host x86_64 machine to flash your Jetson TX1.

1. Go to Nvidia Embedded Download Center and download [JetPack for L4T](https://developer.nvidia.com/embedded/downloads?#?dn=jetpack-for-l4t-2-2).
2. Add exec permission for the JetPack-L4T-${VERSION}-linux-x64.run
  <br>`$ chmod +x JetPack-L4T-${VERSION}-linux-x64.run`
3. Run JetPack-L4T-${VERSION}-linux-x64.run in the terminal on the host ubuntu.
  <br>
  ```
  $ mkdir Programs
  
  $ cd Programs
  
  $ mkdir Jetpack-L4T
  
  $ cd Jetpack-L4T
  
  $ mv ~/Downloads/JetPack-L4T-${VERSION}-linux-x64.run ~/Programs/Jetpack-L4T
  
  $ ./JetPack-L4T-${VERSION}-linux-x64.run
  ```
4. Check the installation directory.
5. Select the development environment to setup.
   E.g. Jetson TK1 Development Kit and Ubuntu Host
        Jetson TX1 (32-bit) Development Kit and Ubuntu Host
        Jetson TX1 (64-bit) Development kit and Ubuntu Host
6. Jetpack installer will pop up a window to ask for permission to use during the installation process; enter your password.
7. Select the Jetson Developer Kit that you would like to install for Jetson TX1. 
8. Accept the license agreement for the selected components.
9. Once the host installation steps are completed, click the Next button to continue with the installation of target components.
10. Select Device accesses Internet via router/switch for network layout.
11. Select eth0 or eth1 depending on your setup for the interface to use for Internet access.
12. A pop-up window will instruct ypu to put your device into Force USB Recovery Mode in order to flash the OS.
    <br>To flash OS,
    - Power down the device. If connected, remove the AC adaptor from the device. The device MUST be powered off, not in a suspend or sleep state.
    - Connect the Micro-B plug on the USB cable to the Recovery (USB Micro-B) Port on the device and the other end to an available USB port on the host PC.
    - Connect the power adaptor to the device.
    - Press and release the Power button to power on device. Press and hold the FORCE RECOVERY button: while pressing the FORCE RECOVERY button, press and release the RESET button: wait two seconds and release the FORCE RECOVERY button.
    - When the device is in recovery mode, open another terminal and type `$ lsusb`.
      lsusb command on host will list a line of "NVidia Corp"
    - Press Enter on previous terminal.
13. Select Next when prompted to install components on the specific target machine, and to compile samples.

##Test Cuda

CUDA FFT Ocean Simulation
```
$ cd ~/NVIDIA_CUDA-<version>_Samples/bin/aarch64/linux/release/
$ ./oceanFFT
```

CUDA Smoke Particles Simulation
```
$ cd ~/NVIDIA_CUDA-<version>_Samples/5_Simulations/smokeParticles
$ ./smokeParticles
```




 


