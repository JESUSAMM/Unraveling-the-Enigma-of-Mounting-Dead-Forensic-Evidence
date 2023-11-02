# ****Identifying the File System: Unlocking Data Structures****

---

## **Introduction**

In the realm of digital forensics, one of the fundamental steps in uncovering the secrets of digital evidence is the ability to decipher the underlying file system. The "Identifying the File System" directory serves as your gateway to mastering this critical aspect of forensic investigations.

A file system is like the language spoken by a storage medium, defining how data is organized, accessed, and stored. By understanding the nuances of file systems, you gain the power to recognize the language of data and unlock its meaning. This directory is your compass to navigate the diverse landscape of file systems and comprehend their unique structures.

**Why Identifying File Systems Matters:**

File systems store and manage data in specific ways, and this organization can vary greatly between different file system types. Identifying the file system used in digital evidence is crucial because it allows you to choose the right tools and techniques for access and analysis.


Command:

We will use a tool named fsstat that is going to show us the file sytem type of the partition. 

With the sector offset in hand, you can now provide it as a parameter when using the **`fsstat`** command. This ensures that **`fsstat`** accurately locates and analyzes the file system within the evidence container.

`fsstat -o <sector> container`

`fsstat -o 2048 evidence_container`

### Example: 

Once we have the sectors of the partitions, we can now try to run the fsstat command to know the filesystem type.
Remember, our sectors are 2048 and 206848 (we get them in the last module).

![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/fefbdc48-0228-478d-bd46-a6811a33aa5c)

- First, run the command in the first partition:
    - Run the command `fsstat -o 2048 <bridge>`
      ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/84a2b85d-706c-4f39-aaf7-ebf37b53af43)
    - As we can see the file system is NTFS

- Now, run the command in the second partition:
      ![image](https://github.com/JESUSAMM/Unraveling-the-Enigma-of-Mounting-Dead-Forensic-Evidence/assets/149633912/646debc0-4340-4e30-b24a-1842f0136a36)
   - And again, we found that the file system is NTFS

  

