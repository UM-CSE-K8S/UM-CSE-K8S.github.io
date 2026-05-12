# How to connect two GPU servers using Infiniband DAC cables



## References: 

- Does not work:  [HowTo Install MLNX_OFED Driver, Jan. 24, 2026](https://enterprise-support.nvidia.com/s/article/howto-install-mlnx-ofed-driver)
- [Installing mellanox ofed drivers for my ubuntu 22.04.5 LTS with kernel version 5.15.0-131-generic](https://forums.developer.nvidia.com/t/installing-mellanox-ofed-drivers-for-my-ubuntu-22-04-5-lts-with-kernel-version-5-15-0-131-generic/322431)
- Goto [nVidia DOCA Download page](https://developer.nvidia.com/doca-downloads?deployment_platform=Host-Server) (the old name is [MLNX_OFED](https://network.nvidia.com/products/infiniband-drivers/linux/mlnx_ofed/). Do not use.)   

  - We need to select: Host Server - DOCA Host - Linux - X86_64 - doca-ofed - Ubuntu - 24.04 - deb(local).  See below ![NVidia OFED Ubuntu Driver Selection Chart](./nvidia-doca-ofed-ubuntu-driver.png)

  - follow the installation instructions: 
```
wget https://www.mellanox.com/downloads/DOCA/DOCA_v3.3.0/host/doca-host_3.3.0-088000-26.01-ubuntu2404_amd64.deb
```
We want to verify the SHA256 checksum by 
```

```

```
sudo dpkg -i doca-host_3.3.0-088000-26.01-ubuntu2404_amd64.deb
sudo apt-get update
sudo apt-get -y install doca-ofed
```


- Update the open source NVidia Driver to [NVidia 595.71.05](https://developer.nvidia.com/datacenter-driver-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=24.04&target_type=deb_local).  This avoid the conflicts between linux header and NVidia driver 595.58 when we install DOCA OFED driver. 

- downloaded [mlxup](https://network.nvidia.com/support/firmware/mlxup-mft/)  and query the NIC card with commands:

``` 
vyl@csegpu1:~/ofed$ lspci |grep mellanox -i
0000:8e:00.0 Infiniband controller: Mellanox Technologies MT2910 Family [ConnectX-7]

vyl@csegpu1:~/ofed$ sudo ./mlxup -d 0000:8e:00.0
Querying Mellanox devices firmware ...

Device #1:
----------

  Device Type:      ConnectX7
  Part Number:      MCX75310AAS-NEA_Ax
  Description:      NVIDIA ConnectX-7 HHHL Adapter card; 400GbE / NDR IB (default mode); Single-port OSFP; PCIe 5.0 x16; Crypto Disabled; Secure Boot Enabled;
  PSID:             MT_0000000838
  PCI Device Name:  0000:8e:00.0
  Base GUID:        9c63c00300abe882
  Versions:         Current        Available     
     FW             28.46.3048     28.47.1026    
     PXE            3.8.0100       N/A           
     UEFI           14.39.0014     N/A           

  Status:           Update required

---------
Found 1 device(s) requiring firmware update...

Perform FW update? [y/N]: y
Device #1: Updating FW ...     
FSMST_INITIALIZE -   OK          
Writing Boot image component -   OK          
Done

Restart needed for updates to take effect.
Log File: /tmp/mlxup_workdir/mlxup-20260512_145143_60339.log
vyl@csegpu1:~/ofed$ 
```