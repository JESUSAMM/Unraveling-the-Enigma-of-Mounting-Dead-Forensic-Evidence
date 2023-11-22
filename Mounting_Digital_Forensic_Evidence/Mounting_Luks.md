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
       
      ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/6a069824-f7cb-4871-ad46-dbe9f9aa5cc8)


&nbsp;
&nbsp;
&nbsp;


- Step 2:
  - Confirm the successful decryption by checking for the decrypted volume using `fdisk`:
    - `fdisk -l | grep /dev/mapper/encrypted_volume`
    -    The output should indicate the decrypted volume under the `/dev/mapper/` directory.
      
           ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/c18b852d-c8bd-49ab-95a7-f5bd06d40b76)


&nbsp;
&nbsp;
&nbsp;


- Step 3:
  - Initially, when trying to mount the decrypted partition as a standard ext4 filesystem, it becomes apparent that the partition is part of an LVM structure.
      > **Info:** If the partition had been a standard ext4 filesystem, we would have concluded the process here, mounting it as usual without the need for additional LVM steps.

     ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/2cddd0c4-4dfd-4582-b396-78294e2a61aa)


&nbsp;
&nbsp;
&nbsp;


- Step 4:
  - Run the command `vgchange` to make sure tha  it is activated.
    - `vgcange -ay`
      > **Info:**  The luksOpen command not only decrypts the LUKS-encrypted partition but also makes the decrypted partition available as a device under /dev/mapper/. Once this is done, the LVM volume group associated with that decrypted partition becomes active, allowing you to access the logical volumes within it.
      
      ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/671572aa-799e-4720-b091-8e6a89f366bb)


&nbsp;
&nbsp;
&nbsp;


- Step 5:
  - Display information about physical volumes, volume groups, and logical volumes with the following commands:
    - `sudo pvdisplay`
    - `sudo vgdisplay`
    - `sudo lvdisplay`
      
       ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/febed095-d0bb-4de7-b8df-3a47cfcfe0b3)

&nbsp;
&nbsp;
&nbsp;


- Step 6:
  - Mount the logical volume:
    - `sudo mount -o ro,noexec /dev/[YourVolumeGroupName]/[YourLogicalVolumeName] /mnt/destination`

     ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/aa48296e-9538-4f8e-9ed3-29851e60a8b2)

&nbsp;
&nbsp;
&nbsp;


        
- **END:**
  -  Once mounted, you can navigate to the mount point to access the contents of the logical volume.
      ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/6ddfb830-ffbf-4db4-8676-55173946666c)

&nbsp;
&nbsp;
&nbsp;


Congratulations! You have successfully activated the LVM volume group and mounted the logical volume within the LUKS-encrypted partition. You are now ready to proceed with your forensic analysis or any required data extraction from the decrypted and mounted file system.


