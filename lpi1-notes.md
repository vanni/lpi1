
# LPI1 - Certification course

## - Section 2 -

#### Interrupts
: An interrupt is an event that alters the normal execution flow of a program and can be generated by hardware 2. devices or even by the CPU itself. When in interrupt occurs the current flow of execution is suspended and interrupt handler runs. After the interrupt handler runs the previous execution flow is resumed.

### Useful commands:

`watch -n1 "cat /proc/interrupts"`

### Different hardware devices

#### Cold plug devices
    expansion cards, pci cards, video cards
### Hot plug devices
    usb, firewire and so on

To show a list of pci devices connected:

`lspci`, `lspci -t`

**Kernel > 2.6** : devices are created dynamically, only the devices connected are shown. Previous Kernels all dev devices were displayed even if not connected.

`ls /dev/sd?`

    sda sdb

### All devices require a driver 

`lsmod` - lists all modules drivers loaded in the system (kernel). Example how to find the driver for pc speakers.

`lsmod |grep pcs*` (to narrow done the search)

- *To remove* an unutilised **mod** (driver) from memory

    `rmmod <module_name>`
- *To install* a modules you need to use the command `insmod` but it requires the full path of the module to be installed and they are found in: /lib/modules/<kerner_version>/kernel/drivers/

Example to look for a driver that I have deleted (**parport_pc**) and I want to reinstall:

To find the module in the current kernel with find:

`find /lib/modules/$(uname -r)/ -iname "*parport*.ko"`

**output**:  /lib/modules/5.8.0-48-generic/kernel/drivers/parport/parport_pc.ko

**To install it**:

`sudo insmod /lib/modules/5.8.0-48-generic/kernel/drivers/parport/parport_pc.ko`

***[Certification question: Know how to use `insmod` and `rmmod`]***

A valide alternative is to use **`modprobe`**

```
modprobe -r <module_name>  -- to delete a module from the system

modprobe <module_name>     -- to install a module form t
```
modprobe is easier to use but it picks up the last kernel folder library.

In the file `/etc/modules-load.d/modules.conf` I can set several specifi parameters to load a specific module, alternatively it can be placed in /etc/modprobe.d

The userspace and normal applications can still access indirectly via the **`sysfs`** which in under **`/sys`**

E.g. `
`
***sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)***

And we can see devices organised by category

cd /sys

ls

>sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)


