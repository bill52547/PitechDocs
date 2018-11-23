# How to install CUDA and libcudnn in ubuntu
-------------
## Install CUDA
1 `Ctrl+Alt+F1` to start command window

2 stop lightdm display service 
```bash
$ sudo service lightdm stop
```

3 uninstall current nvidia drivers 
```bash
$ sudo apt remove --purge nvidia*
```

4 install possible dependencies 
```bash
$ sudo apt update
$ sudo apt install dkms build-essential linux-headers-generic
```

5 disable nouveau drivers
```bash
    $ sudo vi /etc/modprobe.d/blacklist-nouveau.conf
``` 
and insert following contents in `blacklist-nouveau.conf`
```bash
blacklist nouveau
options nouveau modeset=0
```
quit and run
```bash
$ sudo update-initramfs -u
```

6 `sudo reboot`

7 download nvidia CUDA toolkits runfile
https://developer.nvidia.com/cuda-downloads?target_os=Linux

8 Run `sudo sh cuda_10.0.130_410.48_linux.run`, change the version to yours

9 Verify
```bash
$ cd /usr/local/cuda/samples/1_Utilities/deviceQuery
$ make
$ ./deviceQuery
```

## install *libcudnn* library
tutorial https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html

1 download contents https://developer.nvidia.com/rdp/cudnn-download

2 in Download respiratory,
```bash
$ sudo dpkg -i libcudnn*
```

3 Verify

 To verify that cuDNN is working properly on your Mac OS X system, perform the following step.

Run the following command.
```bash
$ echo -e '#include"cudnn.h"\n void main(){}' | nvcc -x c - -o /dev/null -I/usr/local/cuda/include -L/usr/local/cuda/lib -lcudnn
```

If no error occurs, both the header and library are installed and can be located by the nvcc compiler.
 
