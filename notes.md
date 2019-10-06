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
# python sdk
* install dependencies
  ```
  $ pip install boto3
  ```

# identify and access management (IAM)
* PCI compliant
* federated identity
* policies
  - set of permissions
    . effect
    . action
    . resource
    . condition
* identify providers
  - integegrate external identity database
* identities
  - users
    . programmatic access
    . aws management console access
  - groups
    . collection of users
  - roles
    . contains users?

# IAM users
## aws console
### permission summary
  * type: managed policy
    - administratoraccess
    - iamuserchangepassword
### adding groups: admins
  * attach adminstratoraccess policy to admins group
  * add user: bob to the group

## aws cli
  * setting up user Alice via awscli
  ```
  $ aws iam help

  # create user
  $ aws iam create-user --user-name Alice

  # set password
  $ aws iam create-login-profile --user-name Alice --password Password123 --password-reset-required

  # get ARN from admin policy
  $ aws iam list-policies --query 'Policies[?contains(PolicyName `AdministratorAccess`) == `true`] | [*].[PolicyName,Arn]' --output text

  # attach admin to Alice
  $ aws iam attach-user-policy --user-name Alice --policy-arn "arn:aws:iam::aws:policy/AdministratorAccess"

  # change the user's password
  $ aws iam update-login-profile --user-name Alice --password NewPassword123 --password-reset-required

  # create programmatic key
  $ aws iam create-access-key --user-name Alice

  # make group admin
  $ aws iam attach-group-policy --group-name Administrators --policy-arn "arn:aws:iam::aws::policy/AdministratorAccess"

  # add new user to new group
  $ aws iam add-user-to-group --group-name Administrators --user-name Alice

  # add new user Alice to existing group
  $ aws iam add-user-to-group --group-name admins --user-name Alice
  ```
# IAM roles

## norole
## s3 bucket setup
  * create s3 bucket
    - input for bucketname and region
    - accept defaults for other options
  * create a file and upload to s3 bucket
  * creating new user with "AmazonS3ReadOnlyAcces" policy attached to user "roletest"
  * clone repo: https://bitbucket.org/awsdevguru/awsdevassoc.git
  * update config.json file with keys
    - add accessKeyId values
    - add secretAccessKey values
    - add region values
  * verify app.js keys
    - bucket name is correct
    - key aka filename is correct
  * install node
  * install node dependencies 
    ```
    $ npm install
    ```
  * roletest to see if user can access the s3 bucket
  ```
  $ node app.js

    Attempting to get file.txt from bucket: roletest-tn

    Success, file data:
    {
      AcceptRanges: 'bytes',
      LastModified: 2019-10-05T19:53:19.000Z,
      ContentLength: 20,
      ETag: '"0fd4e626a53b0e1a045d4c532df5322d"',
      ContentType: 'text/plain',
      Metadata: {},
      Body: <Buffer 48 65 6c 6c 6f 2c 20 49 27 6d 20 61 20 66 69 6c 65 21 21 0a>
    }

    File contents:
    Hello, I'm a file!!
  ```

## with role
* preferred method to allow temporary credentials to access assets on aws

### create a role in IAM
  * IAM > roles > create role > select aws for trusted entity > search for "AmazonS3ReadOnlyAccess" for policy name > give new role a name "EC2_S3_RO"
  * launch new ec2 instance with new role attached
  * under configure instance, attach newly created role "EC2_S3_RO" to this particular instance
  * add tag: Name -> WithRole
  * launch new instance, ssh, update, and upgrade 
  * clone repo: https://bitbucket.org/awsdevguru/awsdevassoc.git
  * install node and its dependencies
  * run the app.js file
  ```
  $ node app.js
  ```
  * getting meta data from an instance
  ```
  $ curl http://169.254.169.254/latest/meta-data/iam/info

  {
    "Code" : "Success",
    "LastUpdated" : "2019-10-05T20:35:17Z",
    "InstanceProfileArn" : "arn:aws:iam::168420310531:instance-profile/EC2_S3_RO",
    "InstanceProfileId" : "AIPASONVB7YBQNCRLDJAG"
  }
  ```
# IAM permissions
## create user to view billing

* IAM > policies > create policy > service > search "billing" > access level "READ" > name new policy "Billing_RO"
* create group for billing
* create finance group and attach our newly created policy "Billing_RO"
* My Accounts > IAM User and Role Access to Billing Information > Activate IAM Access > update

# IAM Multi-factor authentication
* create new user > attach "AdministratorAccess" policy to the user 
* click on newly created user > security credentials tab > Assigned MFA device 

# virtual pricate cloud
## vpc overview
* networking
  - public & private addresses
  - preserved across reboots
  - multiple IPs can be assigned to an instance
  - define and attach multiple network interfaces to one instance
  - ipv6 supported
* security 
  - security groups
  - network ACL
* examples of aws services that can be launched into a vpc
  - aws data pipeline
  - elastic load balancing
  - rds
  - redshift
  - elasticache
  - ec2
  - elastic beanstalk
  - aws opswork
  - workspaces

## vpc networking and security
* subnets
* route tables
* security groups
* access control lists
* nat gateway
* internet gateway (igw)
* egress only igw
* elastic IP (ec2 instance)
* VPC main route table
### VPC gateway IPSec
### VPC peering
### VPC direct connect

## default vpc review
## vpc creation

## vpc traffic flow demo




