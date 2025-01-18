# Encrypting EBS Volume 
## Objective
This project demonstrates how to create and configure an encrypted Amazon EBS volume for secure use with an EC2 instance. It covers volume creation with AWS KMS encryption, attaching the volume, and preparing it for use by formatting and mounting it.

## Tasks Covered
- Creating an encrypted EBS volume
- Attaching the volume to an EC2 instance
- Verifying encryption
- Formatting, mounting, and verifying the volume
### Creating a Volume
![Creating a Volume 1](https://github.com/user-attachments/assets/987cd914-af2e-4102-9284-790fc49e7095)

This step defines the volume specifications
- The volume type is a General Purpose SSD (gp3) volume
- The volume size is 10 GiB
- The IOPS (Input/Output Operations Per Second) is set to 3000 (minimum for gp3)
- The Throughput is set to 125 MiB/s
- The Availability Zone is us-east-1c, ensuring the volume can be attached to an EC2 instance in the same zone

![Creating a Volume 2](https://github.com/user-attachments/assets/88d4dbcf-f775-4d56-8327-c095a33259ec)

This step ensures the volume is encrypted using AWS KMS
- The default AWS KMS (Key Management Service) key is used (aws/ebs)
- The KMS Key ID and ARN (Amazon Resource Name) are displayed
- A note informs that volumes from encrypted snapshots retain encryption, while unencrypted snapshots require manual encryption

___________________________________________________________________________________________________________
### Attaching Volume to EC2 Instance
![Attaching Volume](https://github.com/user-attachments/assets/c88109d2-5cfe-4c3b-8bce-adb456ec2633)

This step prepares the encrypted volume for use by an EC2 instance. Once attached, the instance can format, mount, and store data securely.
- Under the "Actions" menu, the "Attach Volume" option is selected
- The newly created EBS volume (vol-0ea97370980e7e68e) is available and ready for attachment

![Basic Details when attaching volume to desired instance](https://github.com/user-attachments/assets/6e42e5c2-639f-48ac-bafd-241a3b2842f8)

Before attaching the EBS volume to the EC2 instance, I configured its settings and ensured the correct volume was being attached.

Key details shown in the screenshot:

- **Volume ID:** The unique identifier for the EBS volume being attached.
- **Instance ID:** Identifies the EC2 instance to which the volume is being attached.
- **Encryption Settings:** The encryption status of the volume is displayed, ensuring the volume is encrypted before attachment.
______________________________________________________________________________________________________________
### Verifying Volume is Encrypted
![Verifying Encrypted Volume on EC2 Instance](https://github.com/user-attachments/assets/b96fff7a-afb0-4195-a28d-3272f676af16)

This step ensures that the data stored in the EBS volume is ecnrypted and secure

- `lsbblk`: This comamand lists information about block devices, showing the attached volume at the end of the list
- `sudo file -s /dev/xvdk`: This command checks the content of the device `/dev/xvdk` to identify its type
   - The output of `data` indicates that the volume is unreadable in its current state, which could suggest that it is securely encrypted or contains raw, unformatted data
_________________________________________________________________________________________________________________
### Verifying Volume is Mounted
![Verifying the Mounted Volume](https://github.com/user-attachments/assets/e104e976-6410-45f9-bb41-f2987235b048)

In the final step, the volume is formatted, mounted to a directory, and verified for use on an EC2 instance. 

- `sudo mkfs -t ext4 /dev/xvdk`: This command formats the attached volume with the `ext4` filesystem, making it ready for mounting and storing files
- `sudo mkdir /mnt/ecnrypted_ebs`: This creates a mount point (a folder) in the `/mnt` directory where the formatted EBS volume will be attached
- `sudo mount /dev/xvdk /mnt/encrypted_ebs`: This attaches the newly formatted EBS volume to the `/mnt/encrypted_ebs` directory, allowing you to access it like a regular directory
- `df -h`: This verifies that the EBS volume is mounted correctly by showing its size, usage, and the mount point (`/mnt/encrypted_ebs`)
  
## Lessons Learned
- AWS KMS ensures EBS volumes are encrypted for secure data storage.

- Formatting and mounting a volume is necessary to make it usable on an instance.

- Encryption persists during volume attachment, protecting data at rest.

- Tools like `lsblk` and `df -h` help verify volume status and readiness.

- Matching availability zones is critical for attaching volumes to EC2 instances.
