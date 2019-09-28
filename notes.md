# AWS Developer Associate Topics

---
- EC2
- VPC 
- IAM
- Route53
- Elastic BeanStalk
- Kinesis
- RDS
- DynamoDB
- Lambda
- AWS API
- SQS
- SNS
- AWS SDK
- Security
- S3
- API Gateway
- Cloud Formation
- AWS Developer Tools
  - CodeCommit
  - CodeBuild
  - CodeDeploy
  - CodePipeline
  - CodeStar
  - X-Ray
---

# Cloud Services
* public
  - provider data center

* private
  - your data center

* hybrid
  - combination betweein provider data center and your data center

# Cloud Deployment Benefits
* storage space
* flexible spending
* downtime mitigation
* disaster recovery
* software maintenance
* centralized security management
* automated provisioning
* scalable
* decentralized our environment
* getting close to the user
* speed
* capital expenditure reduction

# Cloud Providers
* on-premise IT
* infrastructure as a service (IaaS)
* platform as a service (PaaS)
* software as a service (SaaS)

## Cloud Services Broker

# AWS Services Overview
---
## areas of focus in this course
### compute
  - ec2
  - ec2 container service
  - lightsail
  - elastic beanstalk
  - lambda
  - fargate
### storage
  - simple storage service (s3)
  - elastic file system (efs)
  - storage gateway
  - glacier
### database
  - relational database service (rds)
  - dynamoDB
  - elasticcache
  - redshift
  - elastic map reduce
### networking & content delivery
  - virtual private cloud
  - cloudfront
  - direct connect
  - route 53
### sec., identity, & compliance
  - identity & access management
  - inspector
  - certificate manager
  - director service
  - key management service
  - aws config
---

### mgmt tools
### analytics
### artificial intelligence
### game dev
### mobile services
### app services
### messaging
### migration
### iot
### business productivity
### dev tools
### contact center
### desktop & app streaming


# aws regions
* regions have can have multipole availability zones
  ** availability zone
      - availability zone make up regions

# setting up a lab
* create trial account
* ssh
* browser
* setup awscli
  ```
  $ pip install awscli
  ```



---
# aws foundational services
* aws cli & sdk
* identify and access management (IAM)
* virtual private cloud (VPC)
* elastic compute cloud (ec2)
* route 53 dns
---

# create programmatic user
* IAM
  - configure programmatic user
    ```
    $ aws configure
    ```
  - make sure to obtain; programmatic user will need this info to configure properly
    1. access key id
    2. access secret key id
  - ec2 subcommands
    ```
    $ aws ec2 describe-instances
    ```
  - human readable output
    ```
    $ aws ec2 describe-instances --output text --query 'Reservations[*].Instances[*].[Placement.AvailabilityZone,Tags[?Key==`Name`].Value | [0], InstanceId, State.Name]'
    ```
# aws-shell
# node.js sdk    
* git clone https://bitbucket.org/awsdevguru/awsdevassoc.git
* take a look at package.json
  - notice how many dependencies are there in the file
  - notice the version aws-sdk is using







