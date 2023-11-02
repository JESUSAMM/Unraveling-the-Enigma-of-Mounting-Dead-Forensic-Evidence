# **Mounting the File System: Accessing Data for Analysis.**

---

## **Introduction**

Once the digital forensic investigator has identified the file system within an evidence container, the next critical step is to mount that file system. Mounting allows you to access the data stored within the file system as if it were a standard filesystem, making it available for analysis and investigation.

In the "Mounting the File System" directory, we will explore the procedures, tools, and techniques necessary to successfully mount file systems of various types. Whether you're dealing with NTFS, ext4, FAT32, or other filesystems, this directory will guide you through the process of mounting with precision.

### Why Mounting Matters

Mounting a file system is a pivotal moment in a digital forensic investigation. It enables you to view, search, and analyze the data contained within the file system, uncovering valuable insights and potential evidence. Understanding how to mount file systems is an essential skill for any digital forensic analyst.

### Mounting Commands for Different File Systems

Depending on the file system used in the digital evidence you're examining, you'll need to use specific commands. Below, you'll find a list of commands tailored to different file system types. Choose the one that matches your case:

- **NTFS:** `sudo mount -o ro,noexec,loop,offset=<offset>,show_sys_files,streams_interface=windows <img> <dest>`
- **HFS, HFS+:** `sudo mount -o ro,offset=<offset>,sizelimit=<partsize> <img> <dest>`
- **EXT3, EXT4:** `sudo mount -o ro,offset=<offset>,noload <img> <dest>`
- **XFS:** `sudo mount -o ro,offset=<offset>,norecovery <img> <dest>`
- **Others:** `sudo mount -o ro,offset=<offset>,noexe,loop <img> <dest>`

### Example:

- Create one directory for each partition:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/6f5e8e42-d99b-421a-952d-affe956175d4)

- Mount the first partition:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/e848a436-f82e-4ba4-9eec-25aa9382bcaf)
   - See the content:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/82e73a1d-49f1-4ff1-ac98-49d4a1f2bdcd)


- Mount the second partition:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/813b7396-378d-462e-a21a-0ed0c67485ce)
  - See the content:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/ae6819d0-6dab-4e48-8b80-d4d73df8aad3)
