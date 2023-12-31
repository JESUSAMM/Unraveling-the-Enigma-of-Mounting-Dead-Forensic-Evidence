# **Mounting the File System: Accessing Data for Analysis.**

---

## **Introduction**

Once the digital forensic investigator has identified the file system within an evidence container, the next critical step is to mount that file system. Mounting allows you to access the data stored within the file system as if it were a standard filesystem, making it available for analysis and investigation.

In the "Mounting the File System" directory, we will explore the procedures, tools, and techniques necessary to successfully mount file systems of various types. Whether you're dealing with NTFS, ext4, FAT32, or other filesystems, this directory will guide you through the process of mounting with precision.

### Why Mounting Matters

Mounting a file system is a pivotal moment in a digital forensic investigation. It enables you to view, search, and analyze the data contained within the file system, uncovering valuable insights and potential evidence. Understanding how to mount file systems is an essential skill for any digital forensic analyst.

**Sector Offset:**

The sector offset is a way to address a specific sector within a storage medium relative to a starting point, often used for forensic analysis.  It is calculated as the sector number multiplied by the sector size (typically 512 bytes). The result is the byte offset from the beginning of the storage device.

**Why Identify the Sector Offset?**

File systems within digital evidence containers may not always start at the very beginning of the container. Instead, they are often located at a certain sector offset within the container. Therefore, knowing the sector offset is essential for targeting the correct location of the file system.

**How to Determine the Sector Offset:**

1. **Start Sector:** Begin by using a tool like **`mmls`** to identify the start sector of the partition or file system you wish to analyze. This start sector represents the sector number at which the file system begins.
2. **Calculating Sector Offset:** To obtain the sector offset, simply multiply the start sector number by the sector size (usually 512 bytes).
    
    For example, if **`mmls`** provides a start sector number of 1000, the sector offset would be 1000 * 512 = 512,000.
    

### Mounting Commands for Different File Systems

Depending on the file system used in the digital evidence you're examining, you'll need to use specific commands. Below, you'll find a list of commands tailored to different file system types. Choose the one that matches your case:

- **NTFS:** `sudo mount -o ro,noexec,loop,offset=<offset>,show_sys_files,streams_interface=windows <img> <dest>`
- **HFS, HFS+:** `sudo mount -o ro,offset=<offset>,sizelimit=<partsize> <img> <dest>`
- **EXT3, EXT4:** `sudo mount -o ro,offset=<offset>,noload <img> <dest>`
- **XFS:** `sudo mount -o ro,offset=<offset>,norecovery <img> <dest>`
- **Others:** `sudo mount -o ro,offset=<offset>,noexe,loop <img> <dest>`

&nbsp;
&nbsp;
&nbsp; 

  Flag:
  - **`- o`** Indicates options for mounting the filesystem.
 
  Options:
  - **`ro`**: Mounts the filesystem in read-only mode.
  - **`noexec`**: Prevents execution of binaries on the mounted filesystem.
  - **`loop`**: Associates the file with a loop device.
  - **`offset=<offset>`**: Specifies the byte offset where the filesystem starts in the image file.
  - **`show_sys_files`**: Displays system files (specific to NTFS).
  - **`streams_interface=windows`**: Allows access to named data streams in a manner compatible with Windows (specific to NTFS).
  - **`sizelimit=<partsize>`**: Sets the size limit for the partition (specific to HFS, HFS+).
  - **`noload`**: Avoids loading the journal (specific to EXT3, EXT4).
  - **`norecovery`**: Skips log recovery during mounting (specific to XFS).

&nbsp;
&nbsp;
&nbsp; 
  

### Example:

- Create one directory for each partition:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/b058f394-16f9-474e-a50c-5d150633d7a0)


  &nbsp;
&nbsp;
&nbsp;

&nbsp;
&nbsp;
&nbsp; 


- Calculate the sector offset of the first partition: 2048 * 512 = 1048576
- Mount the first partition:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/73621c8c-421b-42c7-b20a-198b8d780662)

   - See the content:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/0566fa5b-2304-4ce2-a37e-8e9a7ea58b6f)


&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;




- Calculate the sector offset of the second partition: 206848 * 512 = 105906176
- Mount the second partition:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/df87c866-cf3b-4e6c-829c-daade14e10db)

  - See the content:
  ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/daaf6a6a-624b-44d4-af56-0dc90db8e8a1)

&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;
&nbsp;



## Conclusion

Congratulations, you've successfully completed the process of mounting your first piece of digital evidence! Remember that digital forensics can be a challenging field, and mastering it takes time and practice. Don't be discouraged by the initial complexity; with each new case and experience, you'll become more efficient and confident in your skills.

Digital forensics is a journey of continuous learning, and the knowledge and expertise you've gained here are just the beginning. Keep exploring, keep practicing, and keep uncovering the secrets hidden within digital evidence. You're on the path to becoming a skilled digital forensic investigator!

