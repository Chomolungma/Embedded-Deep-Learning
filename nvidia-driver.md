#How to install Nvidia Driver

1. Download the latest Nvidia Driver from [Nvidia](http://www.nvidia.com/Download/index.aspx?lang=en-us).
2. Press Ctrl + Alt + F1.
3. Login with your username and password.
4. Change Permission of NVIDIA-Linux-x86_64-xxx.xx.run file.
<br>`$ chmod 777 NVIDIA-Linux-x86_64-xxx.xx.run`
5. Stop the X Server
   ```
   # Stop X server
   $ sudo stop lightdm

   # Start X server
   $ sudo start lightdm
   ```
6. Follow the instructions to complete install.

boot into command line mode
http://ubuntuhandbook.org/index.php/2014/01/boot-into-text-console-ubuntu-linux-14-04/
