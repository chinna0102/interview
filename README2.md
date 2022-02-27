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
