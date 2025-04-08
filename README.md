## VM images

* .qcow2 - KVM type Virtual Machines
* .vmdk - VMware and VirtualBox and ESXi
* .vdi - VirtualBox
* .vhdx - Microsoft Hyper-V
* .vhd  - Azure requires fixed size

## Example commands Convert qcow2 to other formats

### Universal Conversion (.img for example)

```bash
qemu-img convert image.qcow2 image.img
```

### Convert for VirtualBox (.vdi)

```bash
qemu-img convert -O vdi image.qcow2 image.vdi
```

### Convert qcow2 to vmdk and make it VMware Workstation Player Compatible

```bash
qemu-img convert -f qcow2 -O vmdk image.qcow2 image.vmdk
```

### Convert qcow2 to vmdk and make it ESXi Compatible (doesn't work with VMware Workstation Player)

```bash
qemu-img convert -f qcow2 -O vmdk -o subformat=streamOptimized image.qcow2 image.vmdk
```

### Covert for ESXi 6 - Create a VMDK version 6 image (instead of version 4) (doesn't work with VMware Workstation Player)

```bash
qemu-img convert -f qcow2 -O vmdk -o adapter_type=lsilogic,subformat=streamOptimized,compat6 image.qcow2 image.vmdk
```

### Convert qcow2 to Microsoft Hyper-V new vhdx format

```bash
qemu-img convert -f qcow2 -O vhdx -o subformat=dynamic image.qcow2 image.vhdx
```

### For Azure (VHD images on Azure must have a virtual size aligned to 1 MB.)

```bash
# requires qemu 2.6+
qemu-img convert -o subformat=fixed,force_size -O vpc image.qcow2 image.vhd
```
