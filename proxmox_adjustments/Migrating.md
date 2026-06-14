#I use Proxmox for my VMs and containers for research, study, and general use. In doing this, I have run into issues with VMs that I have from
#other sources. These are a few things that I have come to use regularly to make sure the VMs/containers work in my setup. While the documentation
#is always helpful, it can be rough to get through sometimes, and searching across discussions takes time. AI can help cut that time down, but I 
#like to have references available to just get through setup on my own.

1. Shrink drive partitions
- To shrink drive partitions download [Gparted live iso](https://gparted.org/download.php)
- Mount the iso as a CD on the BM
- Boot VM and get into BIOS/UEFI settings
- Boot from the CD (iso)
- For simplicity, just use the defaults while the iso boots
- Check your free space on the drives, and shrink as needed in the GUI
    - right click on the drive and set the size
    - when done with all adjustments, click the green check
- Shutdown the VM
- Remove the CD, and you're done
- Export from your current hypervisor, or do whatever you were going to do

2. Export VM images (VMWare Workstation) to move to Proxmox
- Load the VM into VMWare
- Select the VM, click File, and select Export to OVF...
- Move the files (all of them) you exported to your hypervisor
- run the command `qm importovf <VMid> <exported>.ovf <your-storage> && qm importdisk <VMid> <exported>.vmdk <your-storage>`

3. Importing a Windows machine requires more, set things up as below:
- SCSI Controller - VMware PVSCSI
- Leave hard disks alone
- Network Device - vmxnet
- OS Type - Make it match!!!
- Download from [virtio](https://github.com/virtio-win/virtio-win-pkg-scripts/blob/master/README.md)


***Incomplete instructions, will be updating. Very detailed instructions found [here](https://www.wundertech.net/how-to-install-windows-11-on-proxmox/)***
