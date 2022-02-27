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

    

    
    
