# Sleuth-kit-Intro (Forensics-Git,Disko4-Pico-CTF)
Giving an introduction to Sleuth Kit, through the Forensics Git 0-2 and Disko4 Challenges from pico CTF


The Sleuth Kit (TSK) is an open-source collection of command-line digital forensics tools designed for investigating disk images and file systems. 

I'll tackle a series of Pico CTF challenges while using and understanding Sleuth Kit.

**First I'll start with Forensics Git series:**


## Forensics Git 0

Description: 
Can you find the flag in this disk image?
(Remember to download the image)

Hints:
How can you extract the directory from the disk image?

Start by doing reconnaissance on the disk image 

**img_stat - Display details of an image file**


```
img_stat disk1.img

```




<img width="693" height="179" alt="image" src="https://github.com/user-attachments/assets/2377b02a-935e-4352-bd3e-7cc7e5612a2d" />





**mmls - Display the partition layout of a volume system  (partition tables)**

```
mmls disk1.img

```



<img width="1003" height="409" alt="image" src="https://github.com/user-attachments/assets/1b6a8bad-bc1e-40b7-806e-e8bb4f88028e" />




So I have TWO Linux filesystems to investigate:

* Partition 1 → likely main system (002)

* Partition 3 → possibly where the flag is hiding (004)

One thing to keep in mind is that this is a **Physical Disk Image**

A physical disk image is a byte-for-byte, sector-level copy of a physical storage device (HDD, SSD, USB, CD/DVD), encompassing all data, file systems, partitions, and unused or deleted space.

If the disk image in question is a disk image the **mmls** command will give significant output.

If the disk image was a Logical Disk Image an error would output from _mmls_ command.

A logical disk image is a file-based copy of active files, folders, and data within a specific partition or file system, excluding unallocated space. 

Unlike physical images, it focuses on visible data, making it faster, smaller, and ideal for targeted forensic investigations or backing up specific user data while ignoring system overhead.

From the partition layout we learn a number of things:

* DOS Partition Table
* Offset Sector: 0
* Units are in 512-byte sectors (Important when calculating the offset)
* Sector of each partition where they Start and End

Next is listing the contents of the partition, for that I'll use the _fls_ command.

fls - List file and directory names in a disk image.

Targeting the 3rd partition (004), which starts at sector 0001140736

```
fls -o 1140736 disk1.img 
```



<img width="928" height="457" alt="image" src="https://github.com/user-attachments/assets/4fabac63-5783-4b20-b77c-709f5ca91985" />




I want to extract the home directory or rathers what's in it. 

tsk_recover - Export files from an image into a local directory


```
tsk_recover -o 1140736 -d 64770 -e disk1.img ./

```


_-d 64770_  Directory inum to recover from, 64770-home.

-e     Recover all files (allocated and unallocated)



<img width="739" height="329" alt="image" src="https://github.com/user-attachments/assets/23ca128a-3202-4089-8a41-d841c1e76414" />


Now it time to use basic navigation command to find the flag from the _ctf-player_ dir.



<img width="1418" height="675" alt="image" src="https://github.com/user-attachments/assets/c366c93d-d045-47ad-bfca-079c553d31ff" />



