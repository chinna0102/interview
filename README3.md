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

