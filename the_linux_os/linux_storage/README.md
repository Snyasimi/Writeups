## Linux storage management with LVM

Linux has a cool technology known as LVM. This technology is built into the linux kernel.
Logical volume management is a technology that helps with the management of storage in linux systems, LVM allows you to "grow" and "shrink" your storage space using commands, this can be done while a system is operational and without unmounting file systems. It creates an abstraction layer on the physical storage devices like your harddisks(block devices).

LVM is made up several components that work together; These are
- Physical devices
    Physcal devices are the actual harddisk that store the data.
- Physical Volumes
    Physical volumes are the initialized physical devices. Initialized because physical devices are converted to physical volumes before LVM can make use of these. 
    Physical volumes are segmented to physical Extents which are small chunks of data that act as storage blocks.
- Volume groups
    A volume group is a storage pool that is made up of one or more physical physical volumes, the VGs have fixed physical extent size during creation but it possible to modify this value during vg creation by using the `-s SIZE` flag. A PV is allocated to a single VG.
- Logical volumes 
    Logical volumes are the smallest unit,logical volumes are provided as storage devices for applications, users and OSs. A logical volume is created from Volume group. Lv is made up of several Logical extents which are mapped to Physical extents, it possible to map one logical extent to 2 physical extents(mirroring).

#### To create:

##### Physical volumes
This is done by identifying which devices will be used by the LVM. After that you need to initialize them as physical volumes bu running the command

```bash

$ pvcreate /dev/sda /dev/sdb
```
This will initialize the devices as physical volumes and have them ready for LVM.

##### Volume groups
Volume groups are storage pools, in the sence that, you can allocate one or more physical volumes to a single volume group. To create a volume group, you will need to assign physical volumes to a named volume group. You use the command `vgcreate VOL_GROUP_NAME DEVICE-1 DEVICE-2`.

```bash 
$ vgcreate my_volgroup /dev/sda /dev/sdb
 Volume group "my_volgroup" successfully created
```
To specify a physical extent size, you pass it the `-s` flag with the size you prefer.

```bash
$ vgcreate -s 32 my_volgroup2 /dev/sda /dev/sdb
 Volume group "my_volgroup2" successfully created
```


##### Logical volumes

To create logical volumes, you use the `lvcreate` command, you also need to specify the logical volume size, name and which VG should the storage be allocated from.

Logical volumes can be assigned space in two ways.
- Specifying size using extents `-l NO. OF EXTENTS`.
- Specifying size using units `-L SIZE`.

Below is an example
```bash
$ lvcreate -n my_lv -L 250MiB my_volgroup #using unit size

```

```bash
$ lvcreate -n my_lv2 -l 48 my_volgroup2 #using NO. of extents
```

*The default physical exent size is 4MiB, thus physical extent of 48 gives  48\*4 = 192 MIB*

### Creating a File System on Logical volumes

To make use of the allocated space, we'll need to create a file system. creating a file system on logical volumes is the same as creating a file system on a physical device. 
It is possible to make use of tools provided in linux to create file systems. We'll be using the [mkfs utility](https://linuxhandbook.com/mkfs-command/) to help us.

To provide the device path, We can use the traditional `/dev/vgname/lvname` format. Althought there is an alternative to use the kernel device mapper name which takes the format `/de/mapper/vgname-lvname`. 

To create a xfs file system on the `my_lv` logical volume, we can do:

```bash
$ mkfs.xfs /dev/my_volgroup/my_lv

```

To create an ext4 file system on the `my_lv2` logical volume, we do:

```bash
$ mkfs.ext4 /dev/my_volgroup2/my_lv2
```


