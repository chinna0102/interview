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