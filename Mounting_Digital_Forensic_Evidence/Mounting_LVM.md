## Unraveling Logical Volumes

In the realm of storage management, Logical Volumes (LVM) introduce a layer of abstraction that offers flexibility and efficiency in handling disk space. This section explores the concept of Logical Volumes and provides insights into the techniques needed to mount evidence stored within these dynamic storage structures.

### Introduction to Logical Volumes

Logical Volumes are a key component of storage management, allowing for dynamic allocation and resizing of storage space on Linux systems. Unlike traditional partitioning, LVM provides a more flexible approach to managing disk resources, enabling features such as volume resizing, snapshots, and more.

In this section, we'll unravel the intricacies of Logical Volumes, guiding you through the process of mounting evidence stored within this versatile storage abstraction. Understanding Logical Volumes is essential for digital forensic investigators working with Linux systems, where LVM is commonly employed.

Let's embark on a journey to comprehend and effectively mount evidence within Logical Volumes.

### Mounting Logical Volumes: Advanced Techniques

> **Note:** This section assumes that you are already acquainted with the fundamental steps of mounting evidence, including creating the bridge, identifying partitions, and understanding file systems. We won't reiterate these basics in the following explanations.
> **Note 2:** This example will be running with a raw image, so you will not see any bridge step.

- **Step 1:**
  - Run the `mmls` command to list the partitions on the disk. This step helps us identify the partition we'll be working on.
    - `mmls disk_image.img`
        ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/0bae8a07-c6f4-40f7-8717-a3de4b7d96c8)

- **Step 2:**
  - Run the `fsstat` command on each partition to identify the one that contains a Logical Volume Manager (LVM) structure. In this example, let's say it's Partition 3.
    - > **Info:** It's normal if the `fsstat` command returns an error when attempting to identify the file system on the suspected LVM partition. This is expected behavior as `fsstat` may not recognize the LVM structure. In fact, the error message could be an encouraging clue that you are heading in the right direction.
    - `fsstat -o 3780608 disk_image.img`
      
       ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/f441ab22-a7e9-44fa-8655-d0450e1c715d)

  - To further confirm that the partition contains LVM structures, attempt to mount it using the following command:
    - `sudo mount -o ro,offset=<offset> /path/to/lvm_disk_image.dd /mnt/destination`
    -  > **Info:** This command will fail, indicating that the system cannot recognize the LVM2_member file system. This is an additional confirmation that this is the right partition.
       
       ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/90d92e88-12c2-4e97-9410-e4a5872b0514)


 - **Step 3**
   - Now that we've identified the partition containing LVM structures, the next step is to set up a loop device using the `losetup` command. This is essential for accessing the partition as a block device.
     - `sudo losetup --find --show --offset=<offset> /path/to/disk_image.img`
     -  > **Info:** This command creates a loop device and associates it with the specified partition in the disk image.
        
        ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/3fa0314d-d7df-4046-b918-b382a1f37bc3)


- **Step 4**
  -  In LVM systems, volume groups need to be activated before you can work with the logical volumes within them. The `vgchange` command facilitates this activation process.
    - `sudo vgchange -ay`
    -  > **Info:**  This command activates all volume groups on the system, allowing you to access and work with the logical volumes associated with these groups.
      
      ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/74d58f27-79d1-47b8-8282-f0b0d1fb927e)





