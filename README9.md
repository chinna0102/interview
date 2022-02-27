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




