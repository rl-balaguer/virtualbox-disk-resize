
# Guide: Extending Virtual Machine Disk Size (For Ubuntu Server 22.04 LTS)

**Important: Before you begin, make sure to back up your virtual machine to prevent any data loss.**

**Step 1: Turn off the virtual machine** Ensure that the virtual machine is powered off before proceeding with the disk resizing.

**Step 2: Prepare GParted**

*   Download the GParted Live ISO file with a name like "gparted-live-x.x.x-x-amd64.iso".
*   In the VirtualBox host OS, go to VirtualBox > File > Virtual Media Manager.
*   Resize the virtual disk by adjusting the slider.

**Step 3: Mount GParted ISO** In the virtual machine settings, mount the GParted ISO file.

**Step 4: Boot into GParted** Start your virtual machine and boot into GParted using the mounted ISO.

**Step 5: Resize the partition**

*   In GParted, locate your virtual drive partition, e.g., /dev/sda2.
*   Right-click on the partition and choose "Resize/Move."
*   Expand the partition to use all available unallocated space.
*   Confirm the operation by clicking the check mark.
*   Exit the GParted GUI and restart your virtual machine with Ubuntu Server.

**Step 6: Verify the partition size** Open the terminal and run the following commands as the root user:

*   `vgdisplay` (Check that VG Size matches the resized partition size)
*   `lvdisplay` (Verify the LV Size)

**Step 7: Resize the logical volume** Run the following command to resize the logical volume:

bash

```bash
lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
```

**Step 8: Verify the logical volume size** Run `lvdisplay` again and ensure that the LV Size is now larger.

**Step 9: Adjust the volume size** Check the current size of the volume with:

bash

```bash
df -h
```

**Step 10: Resize the volume** Adjust the size of the volume using the following command:

bash

```bash
resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
```

**Step 11: Verify the size** Run `df -h` once more to confirm that the volume size has increased.

**Step 12: Completion** Congratulations! You have successfully extended the virtual machine disk size. The process is now complete.

Please remember that disk operations are critical, and following the steps carefully and backing up data is essential to prevent any potential data loss.
