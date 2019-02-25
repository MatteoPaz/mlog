# Installing CUDA on Ubuntu 18.04 - NVIDIA® GM206GL Quadro M2000

In the following document I explain the passages in order to install the CUDA environment to run machine learning application on the GPU.

The first step was to see if the NVIDIA graphics card has been detected by the operating system. I have run the following command:

```bash
lspci
```

Among all the results, I have obtained:

```bash
01:00.0 VGA compatible controller: NVIDIA Corporation GM206GL [Quadro M2000] (rev a1)
```

Then, I need to understand which driver needs to be installed.

```bash
ubuntu-drivers devices
```

As result, I have obtained: 

```bash
vendor   : NVIDIA Corporation
model    : GM206GL [Quadro M2000]
driver   : nvidia-driver-410 - third-party free recommended
driver   : nvidia-driver-390 - third-party free
driver   : nvidia-driver-396 - third-party free
```

I have decided to install the nvidia-driver-410 as recommended. To downolad the driver, I have used the .deb package:

```bash
sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb
sudo apt-key add /var/cuda-repo-10-0-local-10.0.130-410.48/7fa2af80.pub
sudo apt-get update
sudo apt-get install cuda
```

At a certain point, during the installation you need to insert a password for the Secure Boot: this step is necessary, because it is a verification mechanism for ensuring that code launched by firmware is trusted. 

Furthermore, secure use of UEFI Secure Boot requires that each binary loaded at boot is validated against known keys, located in firmware, that denote trusted vendors and sources for the binaries, or trusted specific binaries that can be identified via cryptographic hashing.

In our case the code is running by the NVIDIA firmware.

At this point you need to reboot the system.

During the boot, you need to make a choice within the following list:

* Continue boot
* Enroll Key
* Enroll Key from Disk
* Enroll Key from Hash

You have to chose "Enroll Key" and insert the password related to the secure boot.

Running the `nvidia-smi` command, you can see the everything is fine!
