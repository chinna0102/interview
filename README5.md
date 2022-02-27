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

