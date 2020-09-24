# Single GPU Passthrough (Fedora)

## ENABLE IOMMU AND UPDATE TO LATEST BIOS

## Installation

sudo dnf install @Virtualization

## Instructions
Put this file in /etc/dracut.conf.d/vfio.conf

add_drivers="vfio vfio_iommu_type1 vfio_pci"

Then you want to run `sudo dracut -f`

----------------------------------------

Then edit your grub config by doing this below.

`sudo nano /etc/default/grub`

Add this GRUB_CMDLINE_LINUX

amd_iommu=on iommu=pt

Then run

`sudo grub2-mkconfig -o /boot/grub2/grub.cfg`

----------------------------------------

Then edit your modprobe.d/vfio.conf file.

`sudo nano /etc/modprobe.d/vfio.conf`

options vfio-pci ids=REPLACE-YOUR-IDS
options vfio-pci disable_vga=1

Please run `lspci -nn` to grab your PCI IDS for your graphics IDs

---------------------------------------

Then edit your `/etc/libvirt/qemu.conf` and then add your user instead of root.

Then edit the `/etc/libvirt/libvirt.conf` make the user libvirt in the config and add rw rights.

---------------------------------------

Then we need the vfio polaris scripts.

https://github.com/azeoix/vfio-single-gpu-passthrough/blob/master/bin/polaris-vfio-startup.sh.txt
https://github.com/azeoix/vfio-single-gpu-passthrough/blob/master/bin/polaris-vfio-teardown.sh.txt

Refer there to add the IDs, you can open up virt-manager and go to pci devices and find the IDs you will need.

--------------------------------

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.
