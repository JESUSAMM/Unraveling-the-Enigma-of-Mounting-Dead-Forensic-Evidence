## Mounting LUKS-Encrypted Drives

In the realm of digital forensics, encounters with LUKS-encrypted drives are commonplace, especially in the context of Linux systems. LUKS, standing for Linux Unified Key Setup, provides a standard format for disk encryption, offering a robust and widely adopted method to secure data at rest.

### LUKS Overview

LUKS serves as the de facto standard for disk encryption on Linux systems. It provides a flexible framework for creating, managing, and unlocking encrypted volumes. LUKS operates by encrypting entire partitions or logical volumes, adding a layer of security that safeguards sensitive information.

As we delve into the intricacies of mounting LUKS-encrypted drives, this section will guide you through the process of unlocking these encrypted volumes and gaining access to the underlying file systems. Let's unravel the mysteries of LUKS together.

### Mounting LUKS Volumes: Advanced Techniques
> **Note:** This section assumes that you are already acquainted with the fundamental steps of mounting evidence, including creating the bridge, identifying partitions, and understanding file systems. We won't reiterate these basics in the following explanations.
> **Note 2:** This example will be running with a raw image of the partition and not of the disk.

&nbsp;
&nbsp;
&nbsp;

> **Note:** In this section, we won't be utilizing commands like `mmls` or `fsstat` because our evidence pertains to a specific partition, not an entire disk. These commands are designed for analyzing disk structures and file systems on complete disks. Instead, we'll focus on tools and techniques more suited for the specific file system within the partition for effective analysis.

&nbsp;
&nbsp;
&nbsp;


- Step 1:
  - Run the `cryptsetup` command to decrypt the partition.
    -  `cryptsetup luksOpen <disk_img> encrypted_volume`
    -  > **Info:**    This command prompts for the LUKS passphrase or keyfile, effectively unlocking the encrypted partition.
       
      ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/91e1190f-688a-4fdc-9947-fa39170fed45)

&nbsp;
&nbsp;
&nbsp;


- Step 2:
  - Confirm the successful decryption by checking for the decrypted volume using `fdisk`:
    - `fdisk -l | grep /dev/mapper/encrypted_volume`
    -    The output should indicate the decrypted volume under the `/dev/mapper/` directory.
      
           ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/9e42d361-454f-43fd-83fd-8ab99fb9c4ab)

&nbsp;
&nbsp;
&nbsp;


- Step 3:
  - Initially, when trying to mount the decrypted partition as a standard ext4 filesystem, it becomes apparent that the partition is part of an LVM structure.
      > **Info:** If the partition had been a standard ext4 filesystem, we would have concluded the process here, mounting it as usual without the need for additional LVM steps.

     ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/74dde9c3-b63b-4a3b-b80f-609d67292076)

&nbsp;
&nbsp;
&nbsp;


- Step 4:
  - Run the command `vgchange` to make sure tha  it is activated.
    - `vgcange -ay`
      > **Info:**  The luksOpen command not only decrypts the LUKS-encrypted partition but also makes the decrypted partition available as a device under /dev/mapper/. Once this is done, the LVM volume group associated with that decrypted partition becomes active, allowing you to access the logical volumes within it.
      
      ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/441afae4-12b7-41af-b098-8b60e8dd4065)

&nbsp;
&nbsp;
&nbsp;


- Step 5:
  - Display information about physical volumes, volume groups, and logical volumes with the following commands:
    - `sudo pvdisplay`
    - `sudo vgdisplay`
    - `sudo lvdisplay`
      
       ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/bcaa4d57-ade2-4fa3-84ff-5c7849cbb5be)

&nbsp;
&nbsp;
&nbsp;


- Step 6:
  - Mount the logical volume:
    - `sudo mount -o ro,noexec /dev/[YourVolumeGroupName]/[YourLogicalVolumeName] /mnt/destination`

      ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/196c7562-076f-4b79-b3ec-e23d9a11d8cd)

&nbsp;
&nbsp;
&nbsp;


        
- **END:**
  -  Once mounted, you can navigate to the mount point to access the contents of the logical volume.
       ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/2df9930a-b624-4c0d-ba10-e4c9dc5727ec)

&nbsp;
&nbsp;
&nbsp;


Congratulations! You have successfully activated the LVM volume group and mounted the logical volume within the LUKS-encrypted partition. You are now ready to proceed with your forensic analysis or any required data extraction from the decrypted and mounted file system.


