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
