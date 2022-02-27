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

    
