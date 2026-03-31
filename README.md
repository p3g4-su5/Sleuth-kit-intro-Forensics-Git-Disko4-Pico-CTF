# Sleuth-kit-Intro (Forensics-Git,Disko4-Pico-CTF)
Giving an introduction to Sleuth Kit, through the Forensics Git 0-2 and Disko4 Challenges from pico CTF


The Sleuth Kit (TSK) is an open-source collection of command-line digital forensics tools designed for investigating disk images and file systems. I
I'll tackle a series of Pico CTF challenges while using and understanding Sleuth Kit.
First I'll start with Forensics Git series:


Forensics Git 0

Description:
Can you find the flag in this disk image?
(Remember to download the image)

Hints:
How can you extract the directory from the disk image?

Start by doing reconnaissance on the disk image 

img_stat - Display details of an image file

img_stat disk1.img



<img width="693" height="179" alt="image" src="https://github.com/user-attachments/assets/2377b02a-935e-4352-bd3e-7cc7e5612a2d" />



mmls - Display the partition layout of a volume system  (partition tables)

mmls disk1.img




<img width="1003" height="409" alt="image" src="https://github.com/user-attachments/assets/1b6a8bad-bc1e-40b7-806e-e8bb4f88028e" />






