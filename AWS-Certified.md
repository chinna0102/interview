MODEL 1
=======
### Layers of Cloud Computing
	1. SaaS (Applications)
	2. PaaS (Programming Environment --> Elstic Banstock,Google App Engine)
	3. Iaas (vm --> AWS)

### Deployment Models
	1. Public (Public All have Access)
	2. Private (Only  One Organization)
	3. Hybrid (Combination of Public and Private)
	4. Communication (Group of Organanizations)

WAY TO ACCESS AWS RESOURCES
=============================
### Types:
		1. AWS CLI
		2. MANAGMENT CONSOLE
		3. SDK's
### 1. Conect AWS Resource by using `CLI`
	1. Download awscli in ubuntu 
		sudo apt install awscli
	2. Config aws in ubuntu system
		aws configure (Before Configure create IAM user) 
	3. Creating a IAM User
		Goto AWS Dashboard --> IAM Dashboard --> Active MFA(Multifactor Authentication)-->
		Users  --> Create/Add user --> Set user Detaails --> Set Permissions --> Create User
	4. Download CSV for user credentiaals
	5. Enter Credentials on awsconfig 
	6. AWS CLI Commands   (https://docs.aws.amazon.com/cli/latest/reference/)

### 2. Connect AWS Resources by using Managment Console
	Go to AWS Console --> Log back on --> Enter Email/Passs

##########################################################################################################################

MODULE-2
========
SECURITY MNAGMENT IN AWS
-------------------------
### Threats
    1. Phishing (Getting Credentials)
    2. Broute force attack
    ## Solution:
        1. MFA (Multi factor Authentication)
        2. AWS STS or Rolesto get a teporary credentils
        3. Unique Username and Password
        4. Enabling Firewalls,Running Antivirus
        5. IAM (Identity and Access Managment --> Manage Identity,resources and permissions)
        6. Detection Control (Identity potential security threats)
        7. Infrastructure Protection (Protect web application filtering traffic)
        8. Data protection (Help customer data,Credentials and work loads from unauthorized access)
    ** Note: AWS is responsible for Security of the Cloud The customer is Responsible for Security in the Cloud **
### Security Managment via IAM
    Main Components in IAM:  ** Note: Don't attached to the policy to Direct the User **
        1. User
        2. Policy
        3. Groups
        4. Roles (Roles help talk to one service to another service --> like EC2 to S3 Internal Communication)
    1. ROOT A/C: 
        When we create AWS Acoount (Email/Password)
    2. ADMINISTRATOR A/C:
        Attach the Administrator policy (--> He can manage the AWS)
    3. POWER A/C;
        Attach to the Power policy (--> He can access all services except IAM)
    4. NORMAL A/C:
        Attach the Roles and Responsibility as per the User requirment
    ** Note: Roles can't attached to the user & Groups, Roles are attached to the resources **
### GROUPS:
    Groups are created managed by the users
    Go to AWS Dashboard --> IAM Dasboard --> User Group --> Add User --> Add Policy __> Create Group
### POLICY:
    # Generate Policy
        # Flow:
        Go to AWS Policy Generator --> Select Policy and Add the Statement ** Add the Condition also (optional) ** --> Generate Policy
    # Types of Policy:
        1. Managed
            1.a AWS Managed
            1.b Customer Managed
        2. Inline
### AMAZON Congnito: (****)
    Amazon Congito provides Authentication, Authorization, and user managment for your web and mobile apps.
    # Roles
        1. User Managment
        2. Authentication
        3. Synchronization
    # Types:
        1. User Pools (sign in through a user pool and receive tokens after sucessful Authentication)
        2. Identity Pools (Exchange user pool tokens through  an identity pool to get AWS Credentials)
        3. Other AWS Services (Use those AWS Credentials to access other AWS service suchas S3, DynamoDB)
    # Uses
        1. Enhanced Security
        2. Cross platform Consistency
        3. Guest and Social Media Logins
        4. MFA and Password Polices
        4. Marketing Analytics

    # Usecase: 
        GE Healthcare uses AWS Congnito for fedarated single sign-on to the Health Cloud for customers.
        Using Amazon Cognito, their customers are able to use their existing credentials and still access GE Healthcare's other health cloud apps.

### AWS GuardDuty:
    It is an intelligent threat detection service that continuosly monitors for any activity to project customers
    (Inteligent threat protection for Accounts and workloads)
        Enable GuardDuty --> Continuosly Analyse --> Intelligently detect threats --> Take Action
    
    # Usecase: Using GraudDuty to Block Suspicious Host
    Flow:
        GuardDuty --> CloudWatch Events --> LambdaFunction --> Amazon DynamoDB --> VPC Network Access control List --> Amazon SNS --> Email Alert
### WFA (Web Application Firewall)
    Its protect web Applications from common web exploints.Its allow only conditions wht we define
    # Flow:
        Users --> WAF --> WebServers
### AWS Shield:
    AWS Shield is managed Distributed Denial of service (DDoS) protection service tht protects application running on AWS infrastructure.It has two levels of Protection.
        1. Standard Protection (It is Available all AWS Customers at no additional cost)
        2.  Advance Protection (It is paid service that provides addtional features,protection and benfits)
### AWS Access Key:
    It is used forverify the identity of theuser or an Application (running on AWS Platform)
    Its consists of Access key id and Secret access key
### KMS (Key Managment Sysytem):
    KMS is envalop Encription (Encript first layer of data by aws nd second layer of dataa by user (Both keys are requiresd when we Encript and Decript the data))
    
    KMS is managed encryption service that enable user to eaisly encript user data (Its Encript and Decrpt the Data)
    Verify the data encription by using the AWS KMS

    ** Note: AWS managed CMK we can't generated and deleted (AWS will be done) and Customer naged key we can crete and deleted **

    # Create a KMS Flow;
        Go to KMS Dashboard --> Customer managment Keys --> Select Symmentric --> Select Administration permissions --> Select User Permissions  --> Finish
        
        Go to S3 --> select Bucket --> Select File --> Server side Enccription Setting --> Enable Encription --> selecct KmS key ARN --> Save Changes
### AWS CloudHSM (Hardware Security Model):
    The entire cryptography key lifecycle from provisioning,Managing and storing to disposing or archiving the key occurs in the HSM
### ROLES:
    Comunicate between two services
    # Usecase
        Attached EC2 to S3 Bucket
    # Flow:
        Create EC2 Instance --> Create IAM Roles --> Attached role to EC2 instance (Action --> Security --> Change IAM Role)
### Billing Alarm:
    Access and analyze and control AWS costs and usage

    # How to create a Billing Alarm
        Go to Billing Dashboard --> Billing preferences --> Click Recevie billing alerts --> Save preferences
        Go to Cloudwatch --> Billing --> Crete Alarm --> Fill the Details --> Select SNS Topic(Create new topic) --> Alarm Name --> Create Alarm
### Config:
    Record and evaluate configuraations of AWS resources
    
    # How to create Config
    Go to config --> Get started --> select services,Buckets and Other services --> Add Role --> Cteate 

######################################################################################################################

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
    
###########################################################################################################################

MODULE-4
========
OBJECT STOREGE OPTION
---------------------

### Traditional Storege:
    # Type of Storeges Tier:
        1. Tier0 (SSD --> Short Term Storege (High Performence /Higher Cost))
        2. Tier1 (RPM HDD --> Short term Storege)
        3. Tier2 (NL HDD --> Long term Storege )
        4. Tier4 (Magnetic Tape or Cold HDD --> Long Term Storege (Low Performence/ Low Cost))
### Cloud Storege:
    Cloud storage is a way of storing digital dara over the internet on servers that can be placed in different regions.
    # WHY :
        1. Scalable
        2. Secure
        3. scalable
        4. Durable
    
### Different storege options in AWS;
    1. Block (Amazon EBS ,Instance Store) --> SSD Ex: Operating System
    2. Object (Amazon S3 , amazon Glacier) --> Magnatic Tape --> Ex: S3
    3. File (Amazon EFS) --> Internal Files and Servers
    4. Data Migration on AWS Cloud (Snowball, Storege Gateway)
### S3 (Simple Storege service):
    1. Its Object type storege
        Object Storege ---> SSD (Solid state Drive) Type

    2. Universal Namespace (Unique)
        Unique Name for Bucket

    3. Unlimited Storege
        No Limit for Storege (We can scalable for Unlimited)

    4. 1 File > 5TB (File Upload limit)
        Data storege is unlimited but one single file is not exceed to 5TB

    5. Version Control system (Track the Changes Every changes and Record & Document the Changes)
        Go to S3 --> Select Bucket --> Properties --> Edit Versioning (Disable to Enable) --> save Changes ( Goto Objects --> Show objects --> Then we see versioning Object files)
        ** Note: Incase we delete/Update the file The versioning will Document the Files**

    6. Cross region Replication (CRR)
        # Flow:
            Goto S3 --> Create a New Bucket --> Go to Source Bucket --> Managment --> Create replication rule --> Update the Details (select the Region,target bucket and select storege type e.t.c) --> Save --> CRR Created.
        ** Note : Existing Files are not showing in Replicas Bucket Then we select the alla file --> Action --> copy --> select the Target Bucket --> copy Files

    7. Storege Tier (Types: S3,IA,G,I,OZ,GDA)
        # How to change the storege class
            Select files in Bucket --> Action --> Edit storege class --> select the storege class --> save Changes

        # Storege types: 
            S3: Standard Storege (No Minimum Duration)
            I: Inteligent Tiering  (MIn 30 Days)
            OZ: Ine Zone Tiering (Min 30 Days)
            G: Glaclear Tiering (Min 90 Days)
            GDA: Glaclear deep archive (Min 180 Days)
    
    8. Life Cycle Managment (Its help to move the files from one storege to another storege type automatically)
        # Flow
            Goto S3 --> Create a New Bucket --> Go to Source Bucket --> Managment --> Ceate Life Cycle Rule --> Update the Requirments (Object requirments when we deleted/updated) --> save  Changes

    9. In S3 we build static websites only 
        # How to create a Static Website in S3
            Goto S3 --> Create a Bucket --> Permissions --> Edit Policy  --> Goto Policy Generator --Enter required Fields (Make Public Access) --> Update the Bucket Policy --> copy the Source code to Bucket (By Using CLI --> aws s3 cp --recursive . s3://idrbt-static-website/) --> Goto Properties --> Static Website Hosting --> Edit (Disable to Enable) --> Save the Changes --> Open the URL (Brose the website)

    ** Note: When ever we create a Bucket Firewall enable automatically **
        
### S3 Security Permissions:
    1. Firewallnavven 
    2. ACL (Access Control Managment)
        # Flow:
            Go to S3 --> Buckets --> Create Bucket --> Upload the file --> Select file --> permissions --> Edit Block public access (On to OFF) --> Go to Objects --> Select Oblect --> Action --> Make Public via ACL

    3. Bucket Policy
        # Flow:
            Go to S3 --> Buckets --> Create Bucket --> Permissions --> Edit Bucket policy --> Goto Policy Generator --> Select the Options --> Generate --> Copy and Update the Policy --> Save Changes
### CDN (Content Delivery Network):(CloudFront)
    A CDN is a network of servers that distributes content from an “origin” server throughout the world by caching content close to where each end user is accessing the internet via a web-enabled device. (Like a Edge)

    A AWS CloudFront is a web service that speeds up the distribution of static and dynamic content to the users.

                    User Request ===> Edge Location =====> Origin Server
    
### SNOWBALl:
    Types:
        1. Snowball
        2. Snowball Edge
        3. Snowball Mobile

    Snowball is a petabyte-scale data transport solution that uses secure appliances to transfer large amounts of data into and out of the AWS cloud

                *** 1 Snowball can Store 80TB ***       
    *** NOte: Snowball only Import/Export in S3 ***

    **** IMPORT/EXPORT Disk:AWS Import/Export Disk trasfer your data directly onto and off of storege devices using Amazon's high speed internal network and bypassing the Internet ****
                                (This is service is Stoped.Its Replaced by a "SNOWBALL")

### STOREGE GATEWAY:
    Acts as a bridge between on-permise software appliance and cloud based storege.Its has three different Types

        *** [Files,Volumes,Tapes] ====> Amazon Storege Gateway =====> [Amazon S3, Amazon Glacier, Amazon EBS Snapshots] ***

        1. Files
            Filegateway provides a virtual file server,which allows user to store and retrive Amazon S3 objects via standard file storege protocols (NFS or SMB)
                NFS: Network file Protocol
                SMB: Server Message Block
            ** We can use all the S3 capabilities (Lifecycle policy,Versioning and CRR) as the files are mapped to object **
            # Flow Process:
                [Applicatio Server ---> (NFS v4.1) ---> File Gateway] ===>(HTTPS) ===> [S3 Standard ---> S3 Standard Infrequent Access ---> Glacier]
                        (Customer Permises)                                                                 (AWS)
            # Usecase Flow: Enable file share for NFS using AWS storege Gateway

        2. Volumes
            Volume Gateway is mounted to your on-permise application servers through internet small Computer System Interface(iSCSI) devices
            The data in the drive is taken as a snapshot and stored in S3 (we use these snapshots to create a volume and atach them to the instance or on-permises server)
            Types of configuration volumes:
                    1. Stored Mode
                        [Application Server --> iSCSI ---> Volume Gateway Appliance("AWS Volume Stored in AWS & On-Permises")] ====> HTTPS =====> [AWS Storege Gateway ----> Volume stored in Amazon S3("AWS Volume Stored in AWS & On-Permises")]

                    2. Cached Mode
                        [Application Server --> iSCSI ---> Volume Gateway Appliance("Fully Manged Cache of frequently used Data")] ====> HTTPS =====> [AWS Storege Gateway ----> Volume stored in Amazon S3("Stored Volume in AWS)"]

            # Flow Process:
                [Application Server ----> iSCSI ----> Volume Gateway] ====> (HTTPS) =====> [storege Gateway bucket in Amazon S3]
                                    (Customer Permises)                                               (AWS)

        3. Tapes
            Tape Gateway provides the cost effective and durable solution to archive the data.It is mounted to your on-permiseapplication servers through iSCSI devices,which is preconfigured with tape drive and media changer

            # Flow Process:
                [Backup Server --> iSCSI ---> (1. Media Charger 2. Tape Drive) ---> Tape Gateway] ====> HTTPS ====> [Virtual Tapes stored in S3 ---> Archived Tapes Stored in Amazon Glacier]

### How to select the `STOREGE SERVICE`:
    1. Block Storege:
        Only one instance at a time but an instance can have many block storeges attached do it.
        # STOREGE SERVICE --> EBS, Instance Store
        # USECASE --> Structured Database, Virtul Volumes
    
    2. Object Storege:
        Users who have access to the bucket "HTTP & HTTPS or API "
        # STOREGE SERVICE --> S3, Glacier
        # USECASE --> archival Data, Public Cloud Storege, Analytics
    
    3. File Storege:
        Multiple Instance Through NFS Protocols
        # STOREGE SERVICE --> EFS
        # USECASE --> Documnet Sharing, Clustered Database

### CloudFront
    Amazon CloudFront is a content delivery service tht works in conjuction other AWS to provide developers with a simple way to distribute content to end users.CloudFront helps to speed up the delivery of  web content across the globe.

    # Create a CloudFront
    *** Flow ***
    Step: 1
        Goto S3 --> Create a Bucket --> Permissions --> Edit Policy  --> Goto Policy Generator --Enter required Fields (Make Public Access) --> Update the Bucket Policy --> copy the Source code to Bucket (By Using CLI --> aws s3 cp --recursive . s3://idrbt-static-website/) --> Goto Properties --> Static Website Hosting --> Edit (Disable to Enable) --> Save the Changes --> Open the URL (Brose the website)
    
    Step: 2
        Goto CloudFront --> Create Distribution --> Fill the  Required Field  (Add Domain name and SSL Certificates) --> Create Distribution

    Step: 3
        Goto Route 53 --> Hosted Zones --> Select Domain Name --> Create a Record --> Fill the Required Fields (CNAME: One Calling to another name) --> Create Record

######################################################################################################################

MODULE-5
--------

Load Balancing, Auto-Scaling, and Route 53
==========================================

### ELASTIC LOAD BALANCER:
    Elastic load Balancer is a load blancing service by AWS, which distributes incoming traffic accross several targets, such as a amazon EC2 instance, Lambda Function,Containers, and Range of Ip Address, in Multiple Availability zone.
    
    ** Types of Load Balancer:
        1. Application Load Balancer (ALB)
        2. Network Load Balancer (NLB)
        3. Gateway Load Balancer (GLB) (Classic Load Balancer)

## Network Load Balancer (NLB)
    
    # Working Flow:
    [End user1,End User2] ---> Internet ---> Elastic Load Balancer ---> [EC2 Instance1,EC2 Instance 2]

    ** Create a Network Load Balancer **
    Step: 1
        Create a 2 Instance (Follow README4.md File to create a Instance)
        ** Install WebServer **
        ~$ sudo yum update -y
        ~$ sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
        ~$ cat /etc/system-release
        ~$ sudo yum install -y httpd
        ~$ echo "<html Content >" > /etc/www/html/index.html
        ~$ sudo systemctl start httpd
        ~$ sudo systemctl enable httpd
        ~$ sudo usermod -a -G apache ec2-user

    Step: 2
        Create a Hosted Zone
        *** Flow ***
            Goto Route53 --> Create a Hostzone --> Fill the Required Details (Domain name) --> Create a Record (Add a Load Balancer --> Note: Add after create the load balancer) --> Create Hosted zone

    Step: 2
        Create a Target Group
        *** Flow ***
            Goto EC2 Dashboard --> Create a Target group --> Fill the Required Details --> Next --> Add Instances --> Create a Target Group

    Step: 3
        Create a AWS Certificate Manager
        *** Flow ***
            Goto AWS Cerficate Manager --> Request --> Fill the Required Details --> Request

    Step: 4
        Create a " Network Load Balancer"
        *** Flow ***
            Goto EC2 DashBoards --> Load Balancer --> Crete load Balancer --> Select Load Balancer type (NLB) --> (Create a Target Group) --> Add SSL certificates --> Create Load Balancer

## Application Load Balancer (ALB):

    # Working Flow:
    [End user1,End User2] ---> Internet ---> WAF (Web Appliction Firewall) --> DNS --> Elastic Load Balancer ---> [EC2 Instance1,EC2 Instance 2]

    # Components of Application Load Balancer
        1. Listeners
        2. Rules
        3. Target Group
        4. Health Check

    ** Create a Appliccation Load Balncer **
    Step: 1 
        Follow Step-1, Step-2, Step-3 in NLB (Network Load Balancer)

    Step: 2
        Create a "Application Load Balancer"
        *** Flow ***
            Goto  Ec2 Instance --> Load Balancer --> Create a Load Balancer --> Select Application Load Balancer(ALB) --> Add SSL Certificates --> Create a Load Balancer
    Step: 3
        Create a "WAF" (Web Application Firewall)
        *** Flow ***
            Goto WAF & Shield --> [ IP Sets --> Create a IP Set --> Fill the required Feilds --> Create IP set ] --> Getting Started --> Create a Web ACL --> Fill the Rweuired fields --> add AWS Resource --> Click Application Load Balancer --> Add --> Add Rules (IP SET)--> Select lready created ipset --> Select Action --> Next -->  Create Web ACL

### AUTO SCALLING:
    AWS 'Auto Scalling" monitors your applications and automaticlly sacles AWS resources that the part of the applictions. 

    # How AWS Auto saclling Work:
        Explore Application --> Discover what we can scale --> Choose what optimize --> Track Scalling As it Happens

    # Auto Scalling Components:
        1. Groups (Amazon scaling Group[ASG] is collection of EC2 Instances)

        2. Launch Components / Launch Template (Using this, an EC2 Auto scaling group launches EC2 Instances [AMI, Instance type,Key pair, Security groups] 2. specify the multiple ASG 3. we can't modify after creating it)

        3. Scalling option (Types)
            1. Maintain a ** Fixed ** number of EC2 Instance in ASG
            2. ** Manually ** specify the change in the Maximun and Minimum or desired Capacity
            3. Performing scaling actions automatically based on Schedule(Time and Date)
            4. Scale based on ** Demand ** by defining parameters that control the scaling
            5. Use ** Predective Scaling ** by combining Amazon EC2 Auto scaling with AWS Auto scaling

    # How to Create a Autoscalling (Work an Image(AMI))
    *** Flow ***
    Step: 1
    *** Create a AMI ***
        Goto EC2 Dashboard --> Select Instance --> Action --> Image & Templates --> Create Image --> Fill the Details --> Create Image

    Step: 2
    *** Create a Launch Configuration ***
        Goto EC2 Dashboard --> Lanuch Configuration [Auto Scaling --> LC] --> Fill the Requirment Details [This details are used for AUto scalling] --> Create Launch Configuration 
    
    Step: 3
    *** Create a Auto Scaling ***
        Goto EC2 Dashboard --> Create a Scalling Group --> Enter name & Select LC --> Configure Load Balancer --> Configure group size and scaling group and policy --> Add Notification --> Tags --> Create Auto Scalling 

### DNS (Domain Name System):
    DNS Translates human-redable names (like facebook,Amazon and 192.168.0.1)  

    # How to Register a Domain Name
    *** Flow ***
        Goto Route53 --> Registered Domains --> Registered domain --> Choose Domain name --> Contact Details --> Verify  and Purchace

###########################################################################################################################

MODULE-6
--------
Database Services and Analytics
===============================

**Connection String for Database: HostName, UserName, Password, Port, DatabaseName**

### RDS Support Database --> All Database OLTP Type of Databases
MySQL
ORACLE
POSTGRES SQL
Microsoft SQL Server
MariaDB
Aurora

## BENFITS
1. M-AZ (Multiple Availabity Zone) --> Incase Primary database is not Active with in 30 sec data read from Secondary Data Type
2. Read Replica (Improve the Performence of the Main Application ) --> **Note**: Secondary database is only for read Only
3. Everyday Backup (Automatic)

## Types of DATABASE

1. OLTP (RDS) --> Where online transaction processing (OLTP) applications typically store data in rows
2. OLAP (REDSHIFT)--> Enterprises used online analytical processing (OLAP) workloads to answer complex questions about their business by filtering and aggregating their data
3. NOSQL (DYNAMODB) --> We can Store Large amount of Data (NoSQL databases enable you to store data with flexible schema and a variety of data models)

#### How to create RDS Dtabase

    **Note: It is Vertical Database Scalling and "No  Autosaclling for RDS"**

    Goto RDS --> Create Database --> Choose database method --> Fill the all required Fields --> 
    Step: 1
        # Create a VPC:
        ** Flow **
            Goto VPC --> Your Vpcs --> Create VPC --> Fill the VPC Settings --> Create VPC

    Step: 2
        # Create a SUBNETS **(We can use this Website for create websites: https://www.davidc.net/sites/default/subnets/subnets.html)**
        ** Flow **
            Goto VPC --> Subnets --> Create a Subnets --> Fill the Subnet Setting Requirments --> Create Subnet

    Step: 3
        # Create a RDS 
        ** Flow **
            Goto RDS --> Create Database --> Choose a database creation method --> Fill the all required Fields (Select Create VPC and SUBNET) --> CreateDatabase

    # How to Connect RDS Database
        RDS Connect 2 different Types. They are
            1. CLI (Command Line Interface)
                ** Flow **
                Step: 1
                    (Istall mySQL in UBUNTU)
                    sudo apt install mysql-client-core-8.0
                
                Step: 2
                    ~$ mysql -h < database-1.c6cgcq7cxuvh.ap-south-1.rds.amazonaws.com > -u < admin > -p 
                    ~$ mysql -h < database Endpoint Name > -u < username > -p

            2. GUI (Grafhical user Interface)
                ** Flow **
                Step: 1
                    ~$ wget -O - -q http://deb.tableplus.com/apt.tableplus.com.gpg.key | sudo apt-key add -
                    ~$ sudo nano /etc/apt/sources.list.d/tableplus.list
                        # And added the following line
                        deb [arch=amd64] https://deb.tableplus.com/debian tableplus main
                    ~$ sudo apt-get update && sudo apt-get install tableplus
                    ~$ sudo apt-get install libfreetype6 libfontconfig1-dev libcairo2-dev libpango1.0-dev
                    ~$ sudo apt-get install tableplus

                    ** pen Tableplus --> Enter Required Fields --> Connect **
        

### DYNAMO DB:

    **Note: DynamoDB is Horizontal Scalling Database**
    Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability.

    Server less (Means we cant perform CRUD Operations) --> DynamoDB --> Table --> [Availabilty Zone 1A, 1B and 1C] 

    # Eventuaal Consistency:
            Eventual consistency is a consistency model used in distributed computing to achieve high availability (If any do the changes in Table the changes applicable in Order [1A, 1B, 1C] 

    # How to  Create  a DynamoDB:
    ** Flow **
        Goto  Dynmo DB --> Create a Table --> Enter the Table Name --> Fill the Required Fields --> Create Table
    
    # How to take Backup Database (Manual Snapshot):
    ** Flow **
        Goto RDS --> select Database --> Action --> Snapshot --> Create snapshot

        **Note: Incase Source database is Deleted the snapshot will be Available(Its taken Manually) **

    # How to create a Replica
    ** Flow **
        Goto  RDS --> select Databse --> Action --> Create Read replica --> Fill the Required Fields --> Create Replica

    # we cn share the Snapshot to  Other Accounts & Take the Backup, Multi-AZ & Restore

### REDSHIFT:
    Amazon Redshift is a data warehouse product which forms part of the larger cloud-computing platform Amazon Web Services
    ** Flow **
    Applications 1 & 2 --> Database (RDS) --> [ETL(extract, transform, and loading)] --> Data Warehouse (REDSHIFT) --> Connect to Analytics (TABELU and e.t.c..)

    # WHY REDSHIFT:
        1. Massive Parallel process (Master - Node and Node - Master)
        2. Columner Storege (Data  Always store in Columns) --> Users retrive very faster
        3. Advance Compression 
        4. its So Expensive

### ELASTI CACHE:
    "Elasti CACHE" is a cache environment used to cache result in order to reduce overhead and latency on database

        Users --> Application --> Elastic Cache (In-Memory Cache Database ) --> Database

    # Types of Elasti Cache:
        1. Redis 
             Step: 1
                # Create a VPC:
                ** Flow **
                    Goto VPC --> Your Vpcs --> Create VPC --> Fill the VPC Settings --> Create VPC

            Step: 2
                # Create a SUBNETS **(We can use this Website for create websites: https://www.davidc.net/sites/default/subnets/subnets.html)**
                ** Flow **
                    Goto VPC --> Subnets --> Create a Subnets --> Fill the Subnet Setting Requirments --> Create Subnet
            
            Step: 3
                # Create a Redis:
                ** Flow **
                    Goto Elasti Cache --> Select Redis --> Crete --> Fill and Select the Required Fields --> Create
            Step: 4
                # Connect a Elasti Cache
                ~$ sudo apt update
                ~$ cd /tmp
                ~$ wget https://download.redis.io/redis-stable.tar.gz
                ~$ tar xvof redis-stable.tar.gz 
                ~$ cd redis-stable
                ~$ sudo apt install make &&  make
                ~$ sudo apt install redis-tools
                ~$ redis-cli -c -h <Redis Endpoint nam> (sudo redis-cli -c -h shazychinnu-redis-001.dgsaso.0001.aps1.cache.amazonaws.com -p 6379)
        2. MemCache-D

### ATHENA: (Interactive Query Service)
    Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. (Athena is Serverless)
    # How to CCreate a Athena
    ** Flow **
        Goto Create a Database/Existing Database --> Goto Athena --> Create Athena (Explore the Query Editor) --> Setting (If first time using we need to specify the Location the S3) --> Wite a Query  in Editor --> Run 
        (We can read and write the data without install Thirdparty Applications) 

##########################################################################################################################

MODULE-8
--------
Networking and Monitoring Services
===================================
 
*** NOTE: AWS is Supplort Only "Class C" Networks

VPC = Virtual Private Cloud
CIDR  =  Classless Inter-Domain Routing (CIDR) is a range of IP addresses a network uses

10.0.0.0/16 ---> 16 eans Number of Host 
    *  First two  bits are reserved in 10.0.0.0/16
    *  remaining having 255 * 255 = 65535 Hosts
    *  last 4 are obtained for AWS
    *  we can creaate subnets (like 10.0.1.0/24, 10.0.2.0/24)

10.0.1.0/24 ---> 
    *  First Three bits are reseved in 10.0.1.0/24
    *  Remaining having 255 Hosts
    *  we can create subnets (like 10.0.1.1/24, 10.0.1.2/24)

### VPC (Virtual Private Cloud):

** Noe: When we create VPC 3 create at Default Created and Remaining we created Manually **
    1. Default Route Table
    2. Access Control List
    3. Security Groups

    4. Internet Gateway
    5. Subnets (By Default all subnets attched to the "Default Route Table" )
    6. Non-Default Route Table

### Create a VPC
    # How to create a VPC
    Step: 1
        # Create a VPC:
        ** Flow **
            Goto VPC --> Your Vpcs --> Create VPC --> Fill the VPC Settings --> Create VPC
    Step: 2
        # Create a Internet Gateway
        ** Flow **
            Goto VPC --> Internet Gteway --> Create InternetGateway --> Fill the Required Fields --> Create 
        # Attached to the Internet Gteway to the VPC

        ** Flow **
            Select Internet Gtaeway --> Action --> Atttach VPC --> Select VPC --> Attched
    Step: 3
        # Create a SUBNETS **Option:(We can use this Website for create websites: https://www.davidc.net/sites/default/subnets/subnets.html)**
        ** Flow **
            Goto VPC --> Subnets --> Create a Subnets --> Fill the Subnet Setting Requirments --> Create Subnet

    ** Note: When we create a Subnets default "Route Table" will be created (The default Route tble attached to the Internet Gatewaay all subnets to be the access to the public Network)

    # Private Network:
        We need to create a Non-Default Route table attached to the subnets which we want to be private Network.

    Step: 4
        # Create a Sample Application
        ** Flow **
            Create a EC2 Instances for web,db --> (Select Network & Subnet what we created) 
             
### Tunneling:

     a tunneling protocol is a communications protocol that allows for the movement of data from one network to another
     Ex:
        VPC (10.0.0.0/16) --> Subnets [(10.0.1.0/24)--> Public, (10.0.2.0/24)--> Private] --> Public Network
    (Incase we need to Connect to Private Network then we use tunneling)

        Users --> (10.0.1.0/24) Public Network --> (10.0.2.0/24) Private Network (Becz (10.0.5.0/24) & (10.0.2.0/24) Both are same Family so  they have Internal Connection)

### NAT: (Network Address Transalation)

    A NAT gateway gives cloud resources without public IP addresses access to the internet
    ** Note: NAT only talk with Private Network **
    # How to create a "NAT Gateway"
    ** Flow **
        Goto VPC --> Nat Gateway --> Create NAT Gateway --> Fill the Required Fields (Note: Attach to the Public Subnet) -->  Create NAT
        Attached to the Route Table to NAT Gateway (We Access to the Internet to Private Network [10.0.5.0/24])
    
### VPC PEERING:
    A VPC peering connection is a networking connection between "two VPCs that enables" you to route traffic between them using private IPv4 addresses or IPv6 addresses

    ** Note: VPC peering does not support transitive peering relationships **

    ** Flow **
            VPC1 (10.0.0.0/16) --> Private (10.0.3.0/24) ===========> VPC2 (192.168.1.0/24) --> Public (192.168.1.0/24)
    
    # How to Connect:
    (How to Connect a  from 10.0.3.0/24(Private) to 192.168.1.0/24(Public))
    Step: 1
        1. Create a VPC1
        2. Create Internet Gateway
        3. Create a Subnet

    Step: 2
        1. Create a VPC1
        2. Create Internet Gateway
        3. Create a Subnet
    
    # How to  Create Peering Connecction
    ** Flow **
    
    Step: 1
    # Create a Connnection between VPC1 & VPC2
        Goto VPC --> Peering Connection --> Create Peering Connection --> select 2 VPC Connections --> Create --> Action --> Accept Request --> Accept

    Step: 2
    # Add a Route Table
        Goto VPC --> Route Tables --> Edit routes --> Add VPC (like 192.168.0.0/24) --> Save
    
### DIRECT CONNECT:
    AWS Direct Connect is a network service that provides an alternative to using the Internet to utilize AWS cloud services.

### CLOUD WATCH: (AWS In-built Monitoring Tool)
    Amazon CloudWatch is a monitoring and management service that provides data and actionable insights for AWS, hybrid, and on-premises applications and infrastructure resources.

    # How to create CloudWatch 
    ** Flow **
    # DASHBOARD:
        Goto CloudWatch --> Dashboards --> Create a Dashboard --> Add a Metric Graph --> Create a widget
    # ALARM:
         Goto CloudWatch --> Dashboards --> Alarm --> Create Alarm --> 

### CloudTrail:
    AWS CloudTrail enables auditing, security monitoring, and operational troubleshooting by tracking user activity and API usage. 
            ** Note: Event History shows the last 90 Days **

### SNS (SIMPLE NOTIFICATION SERVICE):
    An Amazon SNS topic is a logical access point that acts as a communication channel.Amazon SNS enables you to send notifications directly to your customers. 

### TRUSTED ADVISOR:(Optimize Performence & Security)
    AWS Trusted Advisors provides recommendations that help you follow AWS best practices.its provide 5 parameters.They are
        1. Cost Optimization
        2. Performance
        3. Security
        4. Fault Tolarance
        5. Service Limits   

##########################################################################################################################

MODULE-8
--------
Application Services and AWS Lambda
===================================

### APPLICATION SERVISES:
    1. SES (Simple email Service)
    2. SNS (Simple Notification Service)
    3. SQS (Simple Queue Service)
    4. SWS (Simple Workflow Service)

### SES (AMAZON SIMPLE EMAIL SERVICE):
    AMAZON SIMPLE EMAIL SERVICE is Email sending service via Cloud.This is mainly developed for markaters ans developers to send business and transactional emails.
    # PROCESS
        Sender --> SES --> Recipient 
    ** Note: If Email Request is not valid SES forward to the  Notification/Complaint to  the Sender

    # How to Create a SES:
    ** Flow **
        Goto SES --> Verify a New Domain --> Create a Identity --> Domain/Register Mail & Verfify

### SQS (SIMPLE QUEUE SERVICE):
    SQS is a messaging queue service, which handles message or workflows between other components in a system (Nothing Will be lost )

    ** Note: SQS is Pull Base Service **

    # PROPERTIES:
        1. Visibility Timeout Period
            The time-period or Duration we specify for the queue item which when is fetched and processed by the consumer is made hidden from the queue.
    
            ** Note: The main purpose is "Avoid the Multiple consumers,Consuming the same item Repetitively" **
        2. Size
            The Request max size is 256kb

        3. TIME STOREGE
            The Queue is stored in Min 4 Days Default and Max 14 Days After Its Deleted Permanently
            
            ** Note: Before 14 Days The is not success in After time Period the The reuest Queue is Again Visable when the request is success after success the queue delete permanently **

        4. SHORT & LONG POLLING:
            "SHORT POLLING" means call for the message request continuosly and its no queues return an a empty message
            "LONG POLLING" means call for the message request and its no queue in repository wait till the message is received
    # TYPES:
        1. STANDARD
            * The Order request and received request is Different
            * Unlimited Number of Traansaction/sec
            * Guarantee that a message is delivered at least once
            * Ex: Helps to large number of Request

        2. FIFO
            * The Order request and received request is Preserved (First in - First Out)
            * limit 3000/sec
            * Message Delivery only once
            * Stopping a student from enrolling in acourse before registering for an accounnt

    # How to create SQS
    ** Flow **
        Goto SQS --> Create Queue --> Select Queue Type --> Fill the Required fields --> Create Queue

### SNS (SIMPLE NOTIFICATION SERVICE): 
    Amazon SNS enables you to send notifications directly to the customers.AWS SNS supports SMS text messages (Mobile base base Notification)

        Publisher --> Amazon SNS --> SNS Topic --> [Push Notification, Text message, Email]

        **  Note: SNS is a PUSH Based Service **
    
    # Types:
        1. Application to Application (A2A)
        2. Application to Person (A2P)
    
    # How to Create  SNS:
    ** Flow **
        Goto SNS --> Crete a Topic --> Fill the Details Required --> Create a Topic --> Create Subscription --> Add Email/SMS --> Create Subscription

### LAMBDA: (Lambda is a Serverless)
    AWS Lambda is a serverless compute service that runs your code in response to events and automatically manages the underlying compute resources for you.

        ** Note: We can use any Programming Language and Server Less Service **

        Users --> Web Applications --> [1. S3 Bucket 2. SQS] --> VM (Backend Server) --> Database  ==> "Without Lambda"
        ("The User when Upload the Image The Image stored in S3 Dtabase & Queue will be stored in SQS Next The VM (Backend Condition) take the Queue from SQS and Convert From Large Image to Small Image after the Image  stored in Main Database")

        Users --> Web Applications --> [1. S3 Bucket 2. SQS] --> Lambda --> Database  ===> "With Lambda"
            ("In Lambda Function The Queue will call to Lambda Function")
            
    # How to Create a Lambda
    ** Flow **
        Goto Lambda --> Create a Function --> Select the Function & Add fill the Requirment fields --> Create Functon 

    # Add Trigger
        Goto Lambda function --> Click the Function --> Add the trigger --> Select the trigger --> Add

#########################################################################################################################

MODULE-9
--------
Configuration Management and Automation
========================================

### Infrstructure as Code:
    Type of IT setup where Devops teams can Automatically manage and provision the infrastructure for an application through configuration files

### CloudFormation: (Helps to Provisioning and Configuring)

    AWS CloudFormation is a service that gives developers and businesses an easy way to create a collection of related AWS and third-party resources, and provision and manage them in an orderly and predictable fashion.

    *** Note: AWS CloudFormation is one of the key tools in implementing Infrastructure as code ***

    ### Stack:
        Stack is group of resources
    
    # How to Create a Stack
    *** Flow **
        Goto CloudFormation --> Create a Stack --> Select Template --> Create Template Designer --> Create a Design --> Download Template (Local/S3) --> Goto Create a Stack --> Upload a Download Template --> Next --> Enter Template  Name --> Next --> Fill the  Required Details --> Create a Stack

        *** Note: When create a  stcak the Resource will be created Automatically.Incase we delete the stack the resource will bedeleted automatically ***
    
### AWS OpsWorks:
    A Specific task done at a time multiple servers (With help of OpsWork tools,You can do it seamlessly).All we have do is only once deploy the changes, and it will replicate them across all the components.

    *** OpsWorks is a Configuration Managment Tools ***

    AWS OpsWorks mainly 3 Types:
        1. AWS OpsWorks Stack --> `(End-to-end configuration solution with better Automation and Managment Solution)`
        2. AWS OpsWorks for Chef Automate --> `(Configuration managment with community scripts and tooling compatible with chef)`
        3. AWS OpsWorks for puppet Enterprise --> `(Configuration managment with community scripts and tooling compatible with puppet)`

### Elastic Beanstalk:
    Elastic Beanstalk is a web hosting platform offered by Amazon
        (Elastic Beanstack is used as a PaaS for deploying and scaling web application and service)

    # How to Create a Beanstalk
    ** Flow **
        Goto --> Elastic Beanstalk --> Create Application --> Enter the Required fields --> Next --> Modify Capacity --> Create App
    
    ** Note: Its only for Instant and Small Applications not for the Large and Long life Applications **

#######################################################################################################################

MODULE-9
--------
AWS Architecture Design -1
==========================

### AWS Well-Architech Framework:
    A Well-Architech Framework helps to Cloud Architect to buid applications.
        (Reliability, Performence Efficiency, Cost Optimization, Security, Operation Excellence)

    # How to Build:
        1. Build & Deploy Faster
        2. Risk Migration
        3. Make Informed decision
        4. Learn and Practice

### Resilient Architecture:
    Resilient means `Recoverability`. Quickly/Maintain/Regain Functionality

### Synchronus adn Asynchronus Services:
    # Synchronus Communication Service
        Continuos Service like Classic Load Balancer, Application Load Balancer, Auto scalling
    (The Services Continously watching the services and take the decisions)

    # Asynchronus Communication Service:
        Asynchronous communication doesn't require both parties to be present and speaking at the same time
        Ex: SNS, SQS

### Serverless Architecture
    FrontEnd: API Gateway
    BackEnd : Lambda
    Storege : DynamoDB
    Security : VPC
    Three are Serverless (We attached 3 Components they are Serverless Architecture)

### SELECTION
    1. Virtual Machines --> EC2 Instance 
    2. Containers --> ECS, ECR, EKS
    3. Serverless --> Lambda, API GAteway, DynamoDB

    # DATABASE:
        1. RDS          --> Structure and Tablue Data
        2. Aurora       --> MySQL
        3. DynamoDB     --> NoSQL,Documents, Unstructured Data
        4. Elasti Cache --> Improve any  Web Application
        5. Redshift     --> Data analysis and reporting
        6. QLDB         --> Ledger database, Transacctional logs
        7. Keyspace     --> it is for Apache Cassandra
        8. Neptune      --> Graph database service

