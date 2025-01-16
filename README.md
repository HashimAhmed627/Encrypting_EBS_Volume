# Encrypting EBS Volume 
## Objective

## Tasks Covered

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

______________________________________________________________________________________________________________
### Verifying Volume is Encrypted
![Verifying Encrypted Volume on EC2 Instance](https://github.com/user-attachments/assets/b96fff7a-afb0-4195-a28d-3272f676af16)


_________________________________________________________________________________________________________________
### Verifying Volume is Mounted
![Verifying the Mounted Volume](https://github.com/user-attachments/assets/e104e976-6410-45f9-bb41-f2987235b048)


## Lessons Learned
