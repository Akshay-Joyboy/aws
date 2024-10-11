## Managing EBS Volumes in Linux Instances

Launch an EC2 Instance: Start by launching a new EC2 instance.

Connect to the EC2 Instance: Use SSH to connect to your instance.

Check Attached Volumes: Run the command:

```bash
  lsblk
```

This will display all block devices, including hard drives, SSDs, and partitions.

### Create an EBS Volume:

In the AWS Management Console, navigate to the EC2 service and then to Volumes.

Create a new volume in the same availability zone as your instance. Select the appropriate subnet and attach the volume.

#### Attach the Volume:

After creating the volume, select it, go to Actions, and choose Attach Volume.

Select your instance and specify the device name (e.g., /dev/sdf), then attach it.

#### Verify the Attachment: 

Go back to your instance and run lsblk again to see the updated list of attached volumes.

lsblk (Display Block Devices): This command shows all block devices. 

#### You can customize its output with options like:

-f: Show filesystems.

-o: Specify which columns to display.

-J: Output in JSON format.

-p: Show the full device path.

#### Check Disk Space Usage: Use the command:

```bash
df -Th
```
This displays disk space usage in a human-readable format.

Command Breakdown:

df: Reports file system disk space usage.

-t: Shows the type of each filesystem (e.g., ext4, xfs).

-h: Displays sizes in a readable format (KB, MB, GB).

#### Create a Filesystem: To check if a filesystem exists on the attached volume, run:

```bash
file -s /dev/xvdf
```
Replace xvdf with the name_of_device with the actual device name found in lsblk. 

If the output is just "data," there is no filesystem.

#### To create a filesystem, use:

```bash
mkfs -t xfs /dev/xvdf
```
#### Mount the Storage: Create a directory example addvol in your home directory and 

```bash
mkdir ~/addvol
```
### Mount to 
```bash
mount /dev/xvdf ~/addvol
```

## Note that this is a temporary mount and will be lost upon reboot.

### Make the Mount Permanent:

#### To Grab the Mount Point:

```bash
cat /etc/mtab
```
### Copy the last entry, then edit /etc/fstab using a text editor (e.g., vim):

```bash
sudo vim /etc/fstab
```
### Add the entry to ensure it mounts automatically on reboot

#### Resize Volume Size Install:

In the AWS console, select the volume, choose Actions, and then Modify Volume. Increase the size and confirm the change.

#### Back in your EC2 instance, install the necessary package:

```bash
sudo yum install xfsprogs
```
#### Resize the Volume using:

```bash
    sudo xfs_growfs -d /dev/xvdf
```
#### Verify the Increased Size: Check the disk space again using:

```bash
df -Th
```
## Note on Expanding the Root Volume: To increase the root volume, use:

```bash
    sudo xfs_growfs /
```
This summary provides a clear, step-by-step guide for managing EBS volumes in Linux instances.
