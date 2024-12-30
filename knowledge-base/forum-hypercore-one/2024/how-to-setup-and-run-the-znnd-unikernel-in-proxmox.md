Thread: how-to-setup-and-run-the-znnd-unikernel-in-proxmox
0x3639 | 2024-05-17 10:36:28 UTC | #1

## High Level Instructions

***Note: I am still testing these instructions.***

Here's a comprehensive guide tailored for importing the znn.qcow2 image for Zenon Network into Proxmox.

1. **Preparation**:
   - First, ensure you have a directory for storing QCOW2 images on Proxmox. If not present, create one using:
     ```
     mkdir -p /var/lib/vz/template/qcow2
     ```

2. **Download the znn.qcow2 Image**:
   - Download the Zenon Network's znn.qcow2 image from [GitHub releases](https://github.com/EovE7Kj/unikernel-z/releases). Place the downloaded image into the directory you prepared earlier.

     ```
     cd /var/lib/vz/template/qcow2
     wget https://github.com/EovE7Kj/unikernel-z/releases/download/qcow/znn.qcow2 #< this will change so confirm the URL first
     ```

3. **Creating a New Virtual Machine**:
   - In Proxmox, create a new virtual machine (VM) but skip the OS installation step as the QCOW2 image is pre-configured with the znnd unikernel.

![image|690x491](upload://z2ccYvrsar2j2rlz32x3KHx9tk4.png)

![image|690x491](upload://gKLy8LBJIiJAqBhd537fLXoCvkc.png)


4. **Import the QCOW2 Image**:
   - Import the QCOW2 image into your Proxmox system with:
     ```
     qm importdisk VM-ID /path/to/znn.qcow2 local -format qcow2
     ```
   Replace `VM-ID` with the ID of the VM you created.

5. **Configure the Virtual Machine**:
   - Attach the imported disk to your VM via the Proxmox web interface by going to the VM’s "Hardware" tab, selecting "Add" -> "Hard Disk", and choosing the imported disk. Set the bus to VirtIO for better performance.

![image|690x373](upload://t685cKbibyOxd4l3YMFN0PA0o5S.png)

6. **Boot Configuration**:
   - Adjust the VM’s boot order to boot from the imported disk by navigating to "Options" -> "Boot Order".

7. **Launching the VM**:
   - Finally, start your VM. It should boot using the znnd unikernel loaded from the znn.qcow2 image.

## Detailed Setup Instructions 
https://ostechnix.com/import-qcow2-into-proxmox/

-------------------------

build_republic | 2024-05-17 13:27:05 UTC | #2

What is this for?

-------------------------

0x3639 | 2024-05-17 13:32:00 UTC | #3

`znnd` as a unikernel.

-------------------------

