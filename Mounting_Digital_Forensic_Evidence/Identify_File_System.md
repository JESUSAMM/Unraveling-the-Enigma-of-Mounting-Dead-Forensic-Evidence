# ****Identifying the File System: Unlocking Data Structures****

---

## **Introduction**

In the realm of digital forensics, one of the fundamental steps in uncovering the secrets of digital evidence is the ability to decipher the underlying file system. The "Identifying the File System" directory serves as your gateway to mastering this critical aspect of forensic investigations.

A file system is like the language spoken by a storage medium, defining how data is organized, accessed, and stored. By understanding the nuances of file systems, you gain the power to recognize the language of data and unlock its meaning. This directory is your compass to navigate the diverse landscape of file systems and comprehend their unique structures.

**Why Identifying File Systems Matters:**

File systems store and manage data in specific ways, and this organization can vary greatly between different file system types. Identifying the file system used in digital evidence is crucial because it allows you to choose the right tools and techniques for access and analysis.

**Sector Offset:**

The sector offset is a way to address a specific sector within a storage medium relative to a starting point, often used for forensic analysis.  It is calculated as the sector number multiplied by the sector size (typically 512 bytes). The result is the byte offset from the beginning of the storage device.

**Why Identify the Sector Offset?**

File systems within digital evidence containers may not always start at the very beginning of the container. Instead, they are often located at a certain sector offset within the container. Therefore, knowing the sector offset is essential for targeting the correct location of the file system.

**How to Determine the Sector Offset:**

1. **Start Sector:** Begin by using a tool like **`mmls`** to identify the start sector of the partition or file system you wish to analyze. This start sector represents the sector number at which the file system begins.
2. **Calculating Sector Offset:** To obtain the sector offset, simply multiply the start sector number by the sector size (usually 512 bytes).
    
    For example, if **`mmls`** provides a start sector number of 1000, the sector offset would be 1000 * 512 = 512,000.
    

Command:

We will use a tool named fsstat that is going to show us the file sytem type of the partition. 

With the sector offset in hand, you can now provide it as a parameter when using the **`fsstat`** command. This ensures that **`fsstat`** accurately locates and analyzes the file system within the evidence container.

`fsstat -o <sector_offset> container`

`fsstat -o 512000 evidence_container`
