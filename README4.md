MODULE-3
========
AMAZON EC2 (Elastic Cloud Compute)
----------
### Compute Virtualization:
    'Virtualization layer is (also know as Hypervisor) resides between hardware and VMs
    It is technique of abstracting the physical compute hardware and allowing the extension of multiple operating system simultaneously on a single machine or clustered physical machines.'

    Hardware Components(CPU,NIC Card,Memory,Hard Disk) -->  Virtualization Layer (Hypervisor) --> VM (Creating VMs / VMs enables users to run more than one OS)

### EC2 INSTANCE:
    Steps:
        1. Create a AMI( Amazon Machine Image) --> Its is Pacakage like Operating System and AMI Provides the information required to launch the EC2 Instance
        2. Compute Capacity (like T2, M3, R3, D2, GPU)
        3. Networking (VPC)
        4. Specify the Volume (Root/Bootable Volume) --> *** One Single volume maximum size is 16TB ***
        5. Tags (Like a Name)
        6. Security (Firewall)
        7. Key Pair
            UBUNTU/MAC:
                7.1 Public Key --> (Part of OS)
                7.2 private Key --> (User Key) 
            WINDOWS:
                Convert "PEM" File  to "PPK" Format or Download "GIT" Bash
    # Flow:
        Complete 7 Steps --> chmod 777 <keypair name> --> Connect using "SSH"

    # How to change "Instance Type" of EC2 Instnce:
        Goto EC2 Dashboard --> Select Instance --> Stop Instance (We can't change the state when server is running stage) --> Action --> Instaance setting --> Change Instance type --> Select instance type --> Apply

    # How to Attach a "EBS Volume " to EC2:
        Goto Dashboard --> Volume (Elastic Block store --> Volumes) --> Create Volume --> Enter requied GB --> Create --> Select Volume --> Actions --> Attach Volume --> Select EC2 Instance
        # Commands:
        --> ~$ mkfs.ext4 /dev/xvdf
        --> ~$ mkdir /hazeevali
        --> ~$ mount /dev/xvdf /hazeevali

    # How to Create a "EC2 SNapshots":
        Goto EC2 Dashboard --> snapshots (Elastic Block store --> Snapshots) --> create snapshots --> select Instance --> Create Snapshots

### SECURITY GROUP:
    A Security Group, like a virtual firewall, control the traffic for one or more instances.we can attach multiple security groups for instance ("1" is Minimum $ "5" is Maximum) Every security group consists of two components:
        1. Inbond Rule --> Incomming Connection for Security  Group ---> By default all ports are closed (Always Private)
        2. Outbond Rule --> Outcomming connection for security group --> By default all ports are open (Always Public)

    # How to add 'Security Group" After Launch instnce
        # Flow:
            Goto  Instance --> Select instance --> Action --> Security --> Change Security Group --> Add security Group --> save
        
### AMI (AMAZON MACHINE IMAGE):
    AMI provides the information required to launch the EC2 instance
    Users can launch multiple instance with the same configuration from a single AMI

    # How create  AMI for EC2Instance:
        Goto Ec2 Daashboard --> Select Instance --> Action --> Images and Templates --> Create Image --> Enter Imagename --> Create Image

    # How to create a image by using Custom "AMI":
        Goto EC2 Dasshboard --> AMI (Images --> AMI) --> Select AMI --> Launch Instance from image --> Follow EC2 create Steps

### ELASTIC IP:
    It is a reserved public ip address Ip address tht you can assign to any EC2 instance in particular region.

    # How to "Associate Elastic IP" to EC2 Instance:
        Goto EC2 Dashboard --> Elastic IP's (Network & Security) --> Allocate Elastic-ip --> Allocate (Create E-ip) --> Select E-IP --> Actions --> Associate Elastic IP Address --> Select Instance --> Associate

    # How to "Delete" A Elstic IP:
        Goto EC2 Dashboard --> Elastic IP's (Network & Security) --> Select a E-IP --> Action --> Release the IP Address

### HARDWARE TENANCY:
    Tenancy determines owner of the resources. AWS Provides "Two" Types.They are
        1. Shared (Shared Instance servers shared across multiple Users)
        2. Deticated (Deticated Instance ech user will get seperate Hardware)

### ENI (Elastic Network Interface):
    An Elastic Network Interface (ENI) is a virtual network interface that acts a point of interface between VM and network by acttaching a Public IP, Private IP,Security Groups and many more your instances.
    
    Internet ===> [ Elastic Network Interface(ENI) --> (Private IP, Public IP, Security Group , MAC Address)] ===> [VPC --> (Instace1,Instance2)]

    # How to Create a "ENI"
        Goto EC2 Dashboard --> Network Interface (Network & Security) --> Create Network Interface --> Enter Details & Create Network Interface --> Select Interface --> Attach --> Select Instance --> Attach

### EBS (Elastic Block Storege):
    (This type of storege  is mostly used when the data needs to be accessed quickly and is required longterm) 
    AWS Elastic Block Store (EBS) is Amazon's block-level storage solution used with the EC2 cloud service to store 
    persistent data.They are 3 Types:
        1. General Purpose SSD --> (max IOPS is 30000)
        2. Provisioned IOPS SSD --> (Max IOPS is 90000) 
        3. Magnetic Tapes (MT) --> 

    # How to Attach a "EBS Volume " to EC2:
        Goto Dashboard --> Volume (Elastic Block store --> Volumes) --> Create Volume --> Enter requied GB --> Create --> Select Volume --> Actions --> Attach Volume --> Select EC2 Instance
        # Commands:
        --> ~$ sudo file -s /dev/xvdf
        --> ~$ mkfs.ext4 /dev/xvdf
        --> ~$ mkdir /hazeevali
        --> ~$ mount /dev/xvdf /hazeevali

        *** Note: One EBS volume is attached to one EC2 instance Only ***
### HDD (Hard Disk Drive);
    HDD is spinning magnetic hard disk.They are 2 Types
        1. Throughput   Optamized HDD (st1) --> Provide low magnetic-storege
        2. Cold HDD (sc1) --> Infrequently accessed data 

### EFS (Elastic File System):
    There we do't specify the Size (we store data unlimited).
    AWS EFS provides a simple, scalable, file system for general purpose workloads for use with AWS Cloud services on-permises.
    EFS Only support in linux and Mac
    # How to create a EFS:
        # Flow:
            *********** Pending ******************* 

### Types of EC2 Instance:
    1. On Demand Instances
        * Pay only for what we use ,Instance provided on demand

    2. Reserved Instances
        * Capacity reservation for EC2 instance is mde prior.Its is 75% cheaper than on-demand instances

    3. Spot Instaances
        * The spot price tht is in "effect for the time" period your instances are running is paid
            (its only suitable for workloads which are not critical and are tolerant of intteruption)
### AMAZON FSx:
    A File server is a (central) network storege unit mapping data files to let other computers on the same network access the  files

    # Flow (How to create a FSx)
    