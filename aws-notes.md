# PART 1: Classic Managed AWS

### **IAM**

You need to select a region for all services besides IAM and S3

Root user is created with the account and should not be used.

### **IAM**

User, Groups(teams, users) and Roles(machines). 

You apply permissions using policies in JSON to users, groups and roles. A policy has resources events and actions.

IAM Federation is using SAML standard to use your IAM solution for example LDAP active directory.


### **EC2:**


To log into EC2 instance use ec2-user@publlicIP  use -i and then pem file with the key, run chmod 0400 to give the right permissions to the pem file.

Use tag with key Name so you can add a name so it is show in the console.

   * **Security groups:** are logical groups or firewall rules for the EC2 instances. Many to Many relation. Locked down to region. By default all inbound traffic is not allowed and all outbound allowed. You can **reference other security groups** to extend functionality.

   * **Elastic IP** A elastic IP is a public IP that you own and never changes, you can use it to mask failure or if you need a constant IP but is is better to setup DNS names and use random IPs.
       * Use load balancer instead of setting IPs.
       * You get bill for elastic IPs.

   * **EC2 User Data**
Use EC2 user data field to execute programs during provisioning, so you can add your apps to run at bootstrap like installing Apache. Is used to bootstrap the instance and only runs once. Runs with root user. Click Advanced details and paste the script you want.


   * **AMI**
AMI are EC2 OS images, you have Amazon on linux based on Fedora, Red Hat, windows... you can create your own images and then create all your instances with them. You need this if you have proprietary software, extra security or federation is required to access your company LDAP.

      * Customs AMI are made for a specific region.

   * **EC2 Instance Types**
Instance names start with letters to give meaning: R -> RAM, G -> GPU, etc... M are the balanced ones and T the burstable, you have burst credits you can get in advance and if you get a spike, your CPU will burst and handle them until you run out. Credits are given as part of the instance and once used you recover them over time, you will never pay unless you do T2 unlimited. There is T2 unlimited which if you run out of credits then you will be charged. [Read More](https://aws.amazon.com/ec2/instance-types/?trk=1c56dc8e-723c-405d-bc3a-2e3278bcf081&sc_channel=ps&sc_campaign=acquisition&sc_medium=ACQ-P|PS-GO|Brand|Desktop|SU|Compute|EC2|EEM|EN|Text|Non-EU&s_kwcid=AL!4422!3!536323272432!e!!g!!ec2%20instance%20types&ef_id=Cj0KCQjwyYKUBhDJARIsAMj9lkHGlHAuqQlz_I8_JC1s5A4_gJz_GgzaOKY5oDiPU47_4hkvw8nhtn8aAt-8EALw_wcB:G:s&s_kwcid=AL!4422!3!536323272432!e!!g!!ec2%20instance%20types)

* Ec2 are billed per second.

### **Elastic Load Balancers(ELB)**
 ELBs spread load, expose DNS handle failure, SSL termination, cookie stickiness, HA zones and separate public from private traffic.

You can setup private or public ELB.

AWS guarantees HA on the ELB and maintenance. 

* **Classic:**  

  Not recommended. V1. and then you have the v2 version which are application and network load balancers.  

* **Application load balancers**  

  ALB  are level 7 and they can handle multiple http apps even in the same machine, you can use the url or hostnames to balance. It is great for microservices, it support dynamic port mapping to run multiple containers on the same EC2 instance. The new app balancer is much cheaper because it can handle multiple apps. 

  You can bundle multiple ec2 instances into **target groups** that are the same app/route. So you can scale and maintain cookie stickiness. 
  Target Groups may refer to **group of EC2 instances**, **Auto Scaling Groups**, **ECS tasks**, **Lambda Functions**
   

  You can enable **stickiness** for stateful application.

  ALB support HTTP/s and websockcets, classic load balancer does not support web sockets. 

  **Client IP is available via headers**. The application servers doesn't see the IP or Port of the client directly, it is in the **X-Forwarded-For** & **X-Forwarded-Proto** header set by the ELB. This is because the ELB does connection termination including SSL then redirects so the EC2 see the ELB ip, to get the client use the header.

  **Routing Strategies in ALB**: ALB is great for docker because it can route based on port and path
  * Based on URL Path
  * Based on Query Strings
  * Based on hostname & url

  [ALB Supports multiple TLS Certificates with smart selection using SNI](https://aws.amazon.com/blogs/aws/new-application-load-balancer-sni/)


* **Network Load Balancers**

  Network load balancers CLB are level 4, lower level and are for TCP traffic. **Really high performance and low latency.** 


* CLB/ALB both have ssl termination and healthchecks.
* All ELBs have static host names, but not IPs, do not use IPs.
* ELBs can scale but not instantaneously. NLBs see directly see the client IP, ALB use forward headers. 503 error means ELB is running out of capacity.


### **Auto Scaling Groups**
You can use auto scaling to automatically register new instances to the load balancer. Scale out is adding instances and scale in removing. You need to define auto scaling groups ASG and the balancer will use it to register new instances. 

* [**Launch templates**](https://docs.aws.amazon.com/autoscaling/ec2/userguide/launch-templates.html)
ASG needs the same type of info as EC2 including AMI, EC2 user data, EBS volume, security groups, etc.  This can be provided by Launch Templates. 

* **Scaling Configurations:** You also need to specify min, desired and max capacity. You also need to specify the network and subnet settings, the load balancer info. and the scaling policies, that is when to scale in or out. This can be done using Cloudwatch which is the monitoring service in AWS, they do have alarms. so you can trigger scale in/out based on the triggers in the alarms. Some of the alarms can be based on avg cpu usage, number of request in the ELB, network usage, etc. You can also create custom metrics in cloud watch. Even you can scale based on a schedule. 

* **IAM Roles:** IAM roles attached to an ASG will be assigned to the EC2 instances. ASG is free, you pay for the instances. If you create ASG for you instances, with a min number if you terminate them, the AGS will provision a new one to meet the min req. ASG will terminate unhealthy instances. 

Load balancers and ASG are under the menu in EC2. First you need to create a launch template and then the ASG. The template is to create new EC2 instances, so the config is the same as for creating an EC2 instance, this way you enforce that all of them are the same type. When creating a ASG it is recommended that you go to advanced details and select load balancing so it works with the ELB, just select the target group previously created for the ELB. You can reuse the health check for ELB. You can attach and detach instances to the ASG, it is best practice that all ec2 instances are part of an ASG and ASG are part of target group for the ELB. So load balancers and ASG work together.


### **Elastic Block Storage**

EBS is elastic block storage which is a network drive that you can attach to instances while they run, so you keep the data if the instance is terminated or if you want to store data and persist data. 

You can attach the EBS volume to an EC2 instance and then attach it to a different EC2 instance so you keep the same data between instances. 

**How will you move EBS between AZs**? EBSs are **locked to availability zones**. You cannot transfer it between the AZ, you can move it by **taking a snapshot and then copy the data to another AZ.** 


**EBS Categories**: EBS they have a provisioned capacity(size and IOPS).  You can attach multiple volumes to the same instance. you have EBS types such SSD, HDD and the price differs. GP2 are the avg which are cheap and SSDs. You can increase EBS capacity at any time. 

* **SSD**
  * **General Purpose SSD:** Boot Volumes, Virtual Desktop, Dev & Test Environment Single Instance Database
    * **gp2:** 16000 IOPS, 100 Mib/s
    * **gp3:** 16000 IOPS, 250 Mib/s
  * **Provisioned IOP SSD:** Supports Multi Attach. Missing Critical low latency and high throughput
    * **io1:** more than 16000 IOPS, 1000 Mib/s
    * **io2:** more than 16000 IOPS, 1000 Mib/s
    * **io Block Express:** more than 64000 IOPS, 4000 Mib/s
* **HDD**
    * **st1:** 500 IOPS, 500 Mib/s Throughput Optimized HDD, Big Data Processing
    * **sc2:** 250 IOPS, 250 Mib/s Cold Storage, Infrequently Accessed data.

* You can take snapshots to backup data or to transfer between AZ. 
* You can schedule snapshots. 
* You can create an EBS with encryption enabled,  with this all snapshots of the EBS are encrypted. The data between EBS and the instance is transferred encrypted. All volumes created from snapshots are encrypted. Data is encrypted at rest and in flight, it has slow latency. 
* We can create an unencrypted snapshots of unencrypted volumes and enable encrytion during restoration of the snapshot.  
* Some EC2 instances do not have EBS, they use instance store, which means that the root volume is attach to physical drive, not network like EBS, you get better performance but you lose the data on termination and you cannot resize, also backups must be handled by the user. EBS backed are recommended unless you really need the performance. Each EBS volume can be attach to just one instance and one instance can have many volumes.
*  EBS are locked to the AZ, you can migrate by taking a snapshot and copying it. Snapshots use IO and impact performance, take snapshots when the load is low. Although EBS volumes are persisted and you can attach/detach them from instances, by default the EBS volume will be terminated with the instance, you need to click the check box during creation to tell AWS not to terminate the volume. 


### **EFS**: Read from Ipad

### **Route53**
Route 53 is a managed DNS which is a collection of rules and records to help clients reach servers using urls. the most common records are A: url to Piv4, AAAA URL to IPPv6, CNAME for url to url and Alias utl to aws resource. Route 53 can work with public or private domains. It also has load balancing using DNS not IP, called client side load balancing, health checks and routing policies based on geolocation, failover, latency,etc. Use Alias instead of CNAME because it is faster.



### **Relational Database Service(RDS)**
RDS is a relational database managed service, it is a managed relation database, it is a service that manage an underlying RDBMS, not a DB itself like DynamoDB. You can use **Postgres, Oracle, MySQL, MariaDB, SQL Server** and **Aurora** which is AWS proprietary. 

DBs are managed by AWS RDS you so **patching, backups, monitoring, DR, scaling, maintenance. replicas managed by AWS**, etc. but you cannot access directly using ssh because they are AWS managed. 

* **Read Replicas**:

  You can create up to **5 read replicas for RDS across any AZ or region**. **Async Replication** Replication is *async* so there could be a small delay, **eventual consistency**. Replicas can be promoted as its own DB so it can write. Applications must update the connection string to read from replicas, so it is not totally transparent. 

* **Multi AZ**:
  
  Multi AZ is used for DR, it does sync replication between the master an stand by node which is not live, it takes over just if the master fails. It uses DNS failover, so both DBs have the same dns name, this is done transparent by AWS. So AZ replicas are read only live replicas for performance and Multi AZ is standby for HA. RDS uses nightly backups by default with 7 days retention policy, you can restore at any point in time. It also captures logs in real time. You can also do manual snapshot and they will not be deleted. RDS uses encryption at rest using AWS KMS AS 256, you can use SSL for in flight encryption. To enforce SSL it differs on the RDBMS. In Postgres rds.force_ssl=1 to connect to an SSL DB you need to enter the SSL trust certificate that can be downloaded from AWS. You should deploy RDS DBs in a private subnet. They also use security groups like EC2 to enforce who can access. IAM policies are used to control who can manage the DBs.  MySQL and Aurora can leverage IAM users instead of having a separate username and password.


* **Backup Strategies:**
  
  * Transaction Logs: Default retention is 7 days. Can be increased to 35 days.
  * DB Snapshots
  * Full Backups

* **AWS Aurora:**
Aurora is not a full DB, is is based on MySQL and Postgres, so drivers are compatible it is cloud optimized performs up to 5x better and can dynamically grow. Use Aurora if you don't care much about portability. It can have up to **15 replicas and has instant failover** but it is a bit more expensive. Without Aurora you need to setup the replicas and failover. 
  * Supports cross region replication.
  * Automated patch with zero downtime.
  * Writer & Reader Endpoints.


**Elasticache:**
ElasticCache is a managed cache service using **Redis** or **Memcached** to improve read performance or add state to stateless apps such as serverless. They use sharding, multiple replicas, multi az failover, etc. AWS takes care of all maintenance: monitoring, patching, failover, etc. 

Elastic Cache is used a lot with lamba or stateless micro services to use it for session management or JWT token management. Redis is the most popular choice, it is in memory but persistent into disk (async) so it survives restart. Great for user sessions, distributed states, it has pub/sub queue. It has multi az failover. Memcached is 100% in memory, but Redis is more popular. 




**VPC:**
A VPC it is your own private cloud, you can create them inside a region. This isolates you from the rest. Each VPC contains subnets, each subnets is inside an AZ. You usually have private subnets to have the DBs and services and the public ones to have the public HTTP servers. It is common to have several subnets inside each AZ. In public subnets you put: Load balancers, api gateways, files and static content, and authentication. In private you have the servers and databases. Public and private can talk to each other. Public have access to the outside, private don't. You can use a VPN to access your VPC and see all the private network. VPC flow logs are used to monitor the inbound and out bound traffic from your VPC. You can have several VPC in your account, one per region. You can peer VPCs so they look like they are part of the same network even if they are in different regions. 

S3 is the simple storage solution of AWS and the most famous service used for small and big data files. Buckets are object containers that can be folders and files. Buckets must have global unique names although their are defined at a region level. Names must be underscore and not an ip. Objects have keys which is the full file.  Internally there are only objects inside buckets, but the UI offers folders but these are just logical paths which are the keys. The max value of an object is  5TB. More than 5GB you need to use multi part upload. You have meta  data and tags, there is also a version ID because you get versioning, but you need  to enable it.

S3 is a global service that's why the bucket ID is unique, you do not have a region,however when you create a bucket you need to select a region. This is because the bucket will have a unique DNS name and these are global.

File versioning is enabled at the bucket level for all files. If you update a file a new version is created automatically. You can enable versioning at any time, if there are files already their version will be set to null and any changes from there will have a version.

4 encryption methods on s3: SSE-S3 uses keys managed by AWS, SSE-KMS uses AWS KMS service to manage keys, SSE-C you provide your own keys for encrypt, Client side encryption you manage. 

SSE-S3: mamaged by AWS, AES-256, encrypted servers side and must set header x-amz-server-side-encryption:AES256 when you send file to S3, Amazon provides the key.

SSE-KMS: uses KMS service so you have more control on the expiry and audit trail you also need to pass the header. You manage the lifecycle.

SSE-C: server side encryption using your keys that you manage, AWS doesn't store it, so you need to pass the public key in the upload request using headers, because of this you must use HTTPS.

Client side encryption: you encrypt and decrypt AWS doesn't do anything.

AWS exposes https for encrypted data and http for non encrypted. Encryption in flight is called SSL/TLS.

Two types of S3 security user based (IAM policies, based on API calls), Resource Based: bucked policies which is the most used and are wide rules you set in the console. Object ACL finer grain and Bucket ACL. Bucket policies are json files with resources, actions and effect(allow/deny) and principal (account or user). you can grant public access, force objects to be encrypted on upload and grant access to other AWS accounts. S3 supports VPC end points for instances without public access so instances in the private network can access the file. You can have S3 access logs and store them in other buckets. API calls can be logged in cloud trail. MFA can be used for extra security. You can create signed urls which are available for a limited time only. There is a policy generator that you can use to generate JSON policy documents: https://awspolicygen.s3.amazonaws.com/policygen.html 

You can setup websites in S3 using s3-website prefix, make bucket public.

If you request data from another bucket you need to enable cors. Is common to have images in another bucket but you don't want public access but thru website bucket so enable cors to set origin.

S3 uses eventual consistency you can put and read and get an object immediately but if you do a get first and got 404 you may get it right after you put it, same as update or delete.

For the best S3 performance you want the highest partition distribution. Historically it was recommended to have random characters in front of the key name like "g65d_my_folder/" so the data is partition properly. Never use dates as keys since the partition will be very similar. Since July 2018 you don't need random characters and the performance is much better  > 3500TBS but this is not in the exam.

More than 5GB you need multipart uploaded to maximize bandwith and decrease time on retries. CloudFront is used to cache S3 objects. If you are in a different region and need to do a big file upload use S3 transfer acceleration which uses edge location to upload temporally to a local end point improving performance. If you use KMS encryption you may see a small performance decrease because KMS has bandwidth limits.



CLI: You install the CLI using python, then use aws command. First create access keys in IAM and use aws configure to enter credentials. Then start using aws, for example aws s3 ls.

You can use the cli inside an EC2 instance but this is a bad practice, do not use your credentials anywhere. To use the cli in the EC2 use IAM roles which can be attached to EC2 instances, roles come with a policy authorizing what the ec2 can do. You can assign a cli role to ec2 instance to use cli. aws cli is already installed in aws linux amis but do not use aws configure to set the keys, you can set the region if you want. You need to create a role and attached to the ec2 service, once you have the role click on the instance and select attach role.

You can create your own policies and assign them to roles, you can also create inline policies specific for just one role, but this is not recommended.  Policies have versions to track changes.

There is a AWS policy simulator to test your policies. Many commands have the --dry-run option to test calls without being charged, this is perfect to test for permissions.

The STS command line tools is used to decode errors: aws sts decode-authorization-message. You need DecodeAuthorizationMessage permission in the role to run the command.

EC2 instance metadata is a powerful tool so instance learn about themselves and what permissions they need without using an IAM role for that purpose. The metadata is the info about the instance and can be retrieved at http://169.254.169.254/latest/meta-data which is a private IP. This metadata is heavily used for automation and to run scripts.

AWS has a SDK to access its services. Java, Python, Node.js, C++, etc. AWS cli is based on the python sdk. The SDK is used to deal with DynamoDB and other services. To use the SDK use the default credential provider chain in the user directory aws/credentials. You can also use ENV variables not recommended but useful for docker images. Never use credentials in the code. For API calls from the SDK AWS implements exponential backoff so if you make a request and it fails the SDK will automatically retry but each times it waits the double to not overloaded. 

If you have multiple AWS accounts you can use profiles using aws configure -- profile, so you can use the CLI with multiple accounts. 

Elastic Beanstalk is a developer centric simple view to manage your apps which leverages on the existing components like elb, rds, AGS, etc which are easier to manage, it is a CI tool. Beanstalk manages your instances like os, configuration, etc and also runs the deployment strategy defined by you. It is key for ci. It has 3 components: your app, the app version and the environment (test, qa, prod). You can promote a build through the environments or rollback. It is free to use. Many platforms are supported including docker. Each app can have many envs, each env many versions. You can choose web server or worker type (batch). Beanstalk can create a DB but it is better to externalize it since if you delete beanstalk you lose the DB.

Deployment Modes:  

- Single Instance: great for dev, DNS name is Elastic IP

- HA with load balancer: ELB with the DNS name and many instances. Multi AZs. Auto scaling group. 

4 kind of deployments for HA:

- All at once: very fast and simple but small downtime. No additional cost

- Rolling: You update some of instances call bucket and once is healthy move to the next. You are under capacity during the update but no additional cost. It can be a long deployment.

-Rolling with additional batches: like the other but spins new instances to maintain same capacity during the update and then once completed the old ones get deleted. Long deployment and extra cost. You have a new extra bucket, so it cost extra.

- Inmutable: Spins new instances in a new ASG and when done it switch the ASG. zero downtime and brand new instances, high cost because you replicate cluster and it takes long but you get a quick rollback, you just switch to the old ASG.

- Blue/Green: create a brand new environment, test it independently. Then use Route 53 to start directing traffic in bits until you are happy.

You can use EB extensions files to configure the deployment. The directory must in the root of the src code and must be called .ebextensions and the config must be in yaml or json. the extension must be .config like logging.config. You can use these files to modify default setting or to add resources like RDS or DynamoDb. 

There is also a EB cli specify for Elastic Bean and you can eb create, status, etc.to manage environments and versions. Very helpful for CI/CD. Eb relies on CloudFormation which is a service. Usually you resolve dependencies when you install like npm install, but when you have many instances, and you need to do npm install in all of them, it is better to do npm install in one machine and then create the zip file with the dependencies inside.



AWS CI equivalents: Github->CodeCommit, Jenkins->CodeBuild. To deploy you can use BeanStalk or CodeDeploy. AWS CodePipeline is used to orchestrate all the tools CodeCommit, CodeBuild, BeanStalk etc. 

CodeCommit is a private GIT with no size limit and fully managed and secure. You can integrate it with Jenkins. Security: SSH keys, HTTPS (generate credentials), it supports MFA. It uses IAM policies for authorization. Repositories are encrypted at rest using KMS. In transit uses HTTPS. For cross account access do not use ssh keys or aws credentials, use IAM role and then use AWS STS to access. Both github and code commit integrate with CodeBuild. CodeBuild integrates with IAM roles with github you have other users. Github Enterprise is hosted in your servers. CodeCommit UI it is worse. CodeCommit can integrate with AWS SNS for notifications or AWS Lambda or CloudWatch event rules. Alerts for deleting, pushes, you can run AWS lambda functions to respond to events. CloudWatch rules are uses for pull request or when a comment is added. CloudWatch rules uses SNS under the hood.



CodePipeline: CD with visual workflow. Source: Github/CodeCommit, build, load test, deploy (AWS CodeDeploy, BeanStalk). It is made of stages each stage can have sequential or parallel actions. Stages: Build/Test/Deploy/LoadTest... You can define manual approval step.  CodePipeline works with Artifacts. Each stage can create several artifacts which are passed and stored on S3 and passed to the next stage. Each stage changes will generate a CloudWatch event which can trigger sns notifications. CloudTrail can be used to audit AWS API call. You attach roles to pipelines and must have the right permissions to perform the actions.



CodeBuild: build and test like Jenkins. It is fully managed by AWS which handles provisioning and scaling. You pay for the usage only. It uses Docker under the hood and you can create your own images. It is secure, integration with KMS/IAM/VPC... it uses cloud train for audit. 

Takes code from CodeCommit/github. Build instructions are defined in the code in the buildspec.yml file. Outputs log are output to S3 and cloudwatch logs. There are also metrics to monitor and get statistics. You can use cloud watch events and AWS lambda for alerts and notifications that can use SNS. You can reproduce CodeBuild locally to troubleshoot errors. Pipelines can be defined with CodePipeline or CodeBuild itself. CodeBuild support Java, Ruby, Python,Go, Node, .Net, etc.... You can use Docker to use any other platform. You have Source code with the buildspec.yml. CodeBuild will create a image with the code and run it on a container. There is an optional S3 bucket for cache. Artifacts are stored in S3. Logs are saved in S3 and CloudWatch. buildspec.yml must be in the root o the code. You can define env Variables, you can use secrets using SSM parameter store. You define phases: install(dependencies), pre build, build and post build. Artifacts are generates and stored in S3, cache is also based on S3. You can run CodeBuild locally using CodeBuild Agent.

CodeDeploy: deploy app into many EC2 instances which are not managed by Elastic Beanstalk. Similar to Ansible, Chef, Puppet... Each ec2 machine must run the CodeDeploy agent. The agent is continuously pooling AWS codeDepploy for work to do. CodeDeploy sends appspec.yml which has the instructions with the source code, then the app is pulled form GitHub or S3, EC2 will run the deployment based on the yaml instructions and the agent in the EC2 instance will report success/error. EC2 instances are grouped by deployment group (dev,test,qa...). CodeDeploy can be chained into CodePipeline and use artifacts from there or other tools like auto scaling groups. CodeDeploy is more complex than BeanStalk but more flexible and supports blue green deployments but only on cloud, It supports lambda. It doesn't provision EC2 instances so they need to be ready. Deployment configuration: deployment rules for success or failures for example the minimum number of healthy instances.  Compute platform: Ec2 or lambda. Deployment type: in place or blue/green.  IAM instance profile needed to give EC2 the permissions to pull from S3/Github. Application Revision: application code + appspec.yml. Service role: Role for CodeDeploy to perform operations. Target revision: target deployment app version.

AppSpec file: File section: how to source and copy from S3/Github. Hooks: set of instructions to deploy a new version. The order is StopApplication, DownloadBundle, BeforeInstall, AfterInstall, ApllicationStart, ValidateService(it is healthy)



Configs for Code Deploy: one at a time, half at a time, all  at once (quick but downtime), custom.

Failures: instances stay in failed state, new deployments will first be deployed to failed instances. To rollback redeploy old deployments or enable automated rollback.

Deployment Targets: Set of EC2 instances with tags, directly to ASG, mix ASG/tags or customization scripts using ENV variables. BeanStalk uses CodeDeploy under the hood. 

For blue/green deployment there are BeforeAllowTraffic and AfterAllowTraffic hooks to test it is healthy. 

CodeBuild-> buidspec.yml   CodeDeploy-> appspec.yml

AWS OpsWorks is a configuration management service based on Chef that allows managing and deploying complex application stacks on AWS. 



Cloud Formation: Infrastructure as Code. Traditional CI/CD is hard to reproduce in another region or different AWS account. Infrastructure as code is turning infrastructure into code. Automate infrastructure. Cloud Formation is a declarative way to provision infrastructure. We just tell them what we need (Load balancer, security groups, instances, etc) and cloud formation goes and does it for you. No resources are manually created, everything is automated and the declarative code can be in git. Changes in infrastructure are code reviewed. No additional costs just what you provision, you can estimate the cost with templates. You can have your whole environment provision and deleted, companies they do provision the dev envs at 8 and destroy them at 5pm to save costs. Separation of concerns: there are different stacks: vpc, network, and app stacks. There are lots of cloud formation templates with stacks you can reuse. You upload the templates in S3 and cloud formation will read it. Stacks are identified by names and if you delete the stack you delete everything (not good idea to provision your DBs there). There is a cloud formation designer but you can use yaml file with templates for automation using AWS cli. Building blocks: Resources, parameters, mappings, outputs, conditionals and metadata. You can have template helpers with functions. 

Resources are mandatory and there are over 200.  They can reference each other and they represent AWS components. AWS::aws-product-name::data-type-name. Everything you click in the UI manually is translated into the yaml format this way it can be automated. You cannot create things dynamically in Cloud Formation, it needs to be declared in the template.. There are few AWS services not supported but you can use AWS Lambda custom resources to use them. Parameters are used to pass inputs to the template, very useful to reuse templates. So they are like custom fields. Use Fn::Ref function to reference parameters like vpcId: !Ref MyVPC. !Ref can be used to reference other parameters or even reference resources. Pseudo parameters are custom parameters provider by AWS like AWS::AccountId.

Mappings are hardcoded values in the template, great to define env specific values. If you know the values in advance by deriving then from other values like region you can set up safety templates than using parameters. Use !FindInMap function to get values based on keys. Outputs are optional and can be used as inputs to other templates. You need to export them and the you can use them in other templates, console or cli. Each team can own a template like the network team can have the network template and export the vpc id as output for devs to refer. You cannot delete a stack if its outputs are used by other stacks. Use Export: block to export the value using a name, then use !ImportValue using the export name. Conditions: have conditions using equals and other operators. CreateProdResources: !Equals [ !Ref EnvType, prod] ->if prod. So you define conditions and then use Condition: to use it. Intrinsic Functions: !Ref-> reference parameters.  !GetAtt get attributes from resources, like Ref but ref only returns the ID of the resource but getAtt you can get anything. ImportValue-> previously exported. !Join -> join values to create resources. !Sub -> substitute values in Strings. By default is something fails the whole stack gets deleted. There is an options to disable this. If you update and it fails it goes back to previous state. You can check the log to see the messages.



CloudWatch: Metrics, logs , events, alarms. Can send notifications using SNS.

AWS X-Ray: Similar to Istio, has distribute tracing, performance monitor, troubleshooting.

CloudTrail: Internal monitoring and audit changes of resources. 



Cloudwatch has metrics for all services. Metrics belong to namespaces. Dimension is an attribute of a metric, we can have up to 10 per metric. Metrics have a timestamp. We can build dashboard. EC2 comes monitor with metrics every 5 min, if you want faster enable detailed monitor and pay for it. Memory usage is not pushed by default, you need a custom metrics. By default custom metrics are push every one minute. You can enable high resolution to go up to 1s. To send a metric you need to use the API call PutMetricData which uses the exponential back off strategy to handle error throttling. 

Alarms can be attached to auto scaling, ec2 actions, sns notifications... States: OK, INSUFFICIENT_DATA and ALARM. Period: time to evaluate the metric that triggers the alarm, enable high resolution for faster.

Clodwatch logs: log aggregate. apps can send logs using the sdk, agents can run agents to send logs to cloudwatch, most of the services send by default. The logs can best archived in S3 or send to elastic search. You can use filters in cloudwatch. Logs are grouped in group and each app is a stream. You can tail using sdk and also define expiration policies. You need to have proper permission in aim to stream logs. logs are encrypted at a group level using kms.

Cloudwatch Events can be schedule: as cron jobs, event pattern rules in cloudwatch. You can call lambda functions, send sns notifications, etc. They use json format.



AWS X-Ray. Distributed tracing, logging and monitoring. Troubleshoot performance, understand dependencies, review requests, bottlenecks, etc. It is compatible with many services. Each trace has several segments, one for each call. You can add annotations to the traces.  You can trace every requests or aggregate them. There is IAM access control and KMS encryption at rest. Your code must use X-ray sdk. You need a small code modification not like Istio. The code snippet will capture: AWS calls, http calls, database calls, sqs calls, etc. You need to also install x-ray daemon or enable the AWS integration for x-ray. AWS lambda and other services already run the daemon. You need IAM write rights to send data to x-ray. Make sure that Lambda has the proper role. For EC2 besides the role you need the daemon.



AWS cloud trail provides governance, compliance and audit for your account. It is enabled by default. You get a history in the console from any change in the console, sdk, cli or AWS service. You can put logs from cloud trail into cloud watch. If a resource gets deleted you can find the event in cloud trail and see what happened. Everything you do in AWS is tracked here, great for audits.

AWS has Amazon ES which is the elastic search and Kibana offerings that can be used to analize cloud watch logs. Athena big data analysis tool can also query logs.

AWS config is a fully managed service that provides resource inventory, config history, config change notifications and more. 



Messaging

SQS for queue model, SNS for pub subscribe and Kinesis for stream processing, these are ways to decouple service calls  using async calls, this extra queue layer is great for back pressure, if you get  a spike in traffic the queue will hold messages so the receivers will not go down. 

SQS: 3 types of queues. Standard: fully managed, oldest offering, scales from 1 to 10.000 messages per second and holds them for 4 days by default and 14 max. Low latency < 10ms, horizontal scaling using consumers. It may be duplicate messages and out of order. Max size message is 256kb. Delay queue: can delay messages up to 15min, default is 0. DelaySeconds parameter. It has a body and then key value properties called meta data. In SQS consumers poll the data and can receive up to 10 message at a time. Consumers must process the messages within the visibility timeout period, the delete the message with the ID and a delete handle function. If there are multiple consumers each one will get the message one by one and the consumer needs to process it within the visibility timeout during this time other consumers will not see it. After the time out they will. the default timeout is 30 sec and the max 12 hours. If the operation is idempotent set it low for performance and if one message takes too long it will get process more than one. If not, you can still use the ChangeMessageVisibility API which allows you to request more time. Dead Letter Queue: 3rd type, failed messages go back to the queue in the standard queue, if the problem is the message a loop will be created, you can set a redrive  policy to stop the loop and then use the dead letter queue to send error messages.  To avoid many api calls you can enable long poling up to 20 seconds where consumer will wait if there are no messages. Set WaitInSeconds to set the value. They charge per api call so long poling is cheaper. FIFO queue is newer queue not available in all regions, less throughput < 300 but exactly one warranty and order. You can set consumer groups based on content and have automatic de duplication based on the body hash.

For large messages use SQS extended client that leverages on S3, body is encrypted but not metadata, so do not put sensitive data. No VPC end point for SQS, you need internet connectivity. PurgeQueue to delete all messages in queue. There is a batch API you can use to decrease cost.

SNS: pub subscribe. a producer sends a singe message to a topic and many subscribers consume the topic, subscribers can be SQS, http end points, lambda, email, sms, push notifications. It integrates with many services: Cloudwatch, cloud formation, s3, etc. You need mobile sdk to send push notifications. A common pattern is the SNS + SQS fan out where you put a message once in SNS and this is sent to many SQS queues. This is the overcome the problem that SNS doesnt hold the messages and SQS does. 

Kinesis is a managed alternative to Kafka, although recently they released KMS managed kafka since it is better than kinesis. Compatible with Spark. It is HA using 3 AZs.It has several APIs like Kafka: streams, analytics (ksql) and firehorse(connect). Retention from 1 to 7 days. You can replay data. You need to define shards(partitions) in advanced and you are billed per shard. You can batch calls. Hot partition problem is when you use a key that is not evenly distributed so most of the messages go to the same partition. You can use SDKs or cli. ProvisionThroughputExceeded is thrown is you sent too many messages, just retry, add more shard or make sure you dont have a hot partition. Besides the SDK you can use the client library KCL which uses DynamoDB to track the offsets. Data Base64 encoded. You can use Kinesis inside your VPC. Data Analytics: real time sql, can create new streams, you pay for the data you consume, it has auto scaling. Firehorse is for ETL, a bit more latency, many data formats but you pay for conversion. You pay for data. SQS and Kinesis consumer pull data and SNS they get push. Kinesis only one consumer per shard. You must provision your throughput in advance for Kinesis not in SQS.



PART 2: SERVERLESS

It is anything that doesn't require managed infrastructure. Started with Lambda and Faas but now it has authentication and storage like DynamoDB. The idea is that you don't deploy services but code as functions, or in DB, you do not manage a database just store data. EC2 you need to provision in advance, they are continuously running, you need to bootstrap them and do other management. You are limited by RAM and CPU. 



Lambda are virtual functions that run when called and they automatically scale without intervention, they are short lived and you pay per usage. It integrates with many services and it is the glue between them based on events. Supports many languages and it is integrated with cloud watch for monitoring. You need to define the RAM in advance but it is easy to get and it is based on the code not load. It is very cheap. Functions have roles to define what can they do in the AWS infrastructure. 

Configuration: timeout is the max execution time, by default is just 3 seconds. Max 300. You send ENV variables, set RAM, you can deploy in your VPC. Lambda functions can have up to 1000 parallel executions. You can set reserve concurrency to lower the value, once the max is passed throttling takes place. Throttle error is 429. You can run the functions async and they will retry 2  times after that they go to the DLQ queue which can be SNS or SQS. You need to add SNS and SQS permissions to the role to write to the queue. Lambda is integrated with X-ray. You can write to tmp folder up to half GB. If you upload a function it must be a zip file up to 50mb and uncompress 250mb. Functions have versions. $LATEST is the last one which is mutable, then you publish a immutable version. a version is the code and configuration. Aliases are pointers to lambda versions this way you can have your dev,test, prod environment and point them to different function versions. You can do blue green and canary deployments with lambda and assign certain percent of traffic to different versions. So users interact with the same arn and you can rewire the aliases. Do heavy work like connect to DBs outside the handler otherwise you will re initialize the connections. Use env variables, do not hard code urls. Encrypt passwords with KMS. Break down big functions. do not use recursions and VPC is slower so try to avoid. Lambda invocation type: RequestResponse sync or Event async. Increased RAM will also allocate more CPU and network bandwidth.

The code package is stored in s3 and on first invocation the code is pull and a set of containers are created using cloud formation, this enables hot invocations.

It is common to write lambda functions for ci/CD that do integration test simulating event sources using the invoke api, or functions that update the aliases, this is done thanks to events trigger by code pipeline that can call lambda.

AWS CodeStar is a unified UI for creating serverless apps using best practices. It comes with a pre build pipeline for serverless apps.It comes with member management, issue tracking and operations.



Dynamo DB: NoSQL, no direct supports for joins or aggregations like join, no relational data but distributed horizontal scaling which is great for lambda. By default Dynamo is highly available using 3 AZs. Highly scalabable and serverless, you do not manage it. Millions of request per seconds, fast and consistent performance, integrated with IAM. You can do event driven programing using Dynamo Streams. Very low cost and auto scaling.

DynamoDB is made of tables each one with a primary key, each table has infinite number of items (rows), each item has attributes similar to columns but they can be nested and can be added over time, you can have list and maps as attributes. Primary key two options: partition key only, this is a hash like Kinesis, must be evenly distributed. The second option is having a combination of a primary key and sort key, the combination must be unique, data is grouped by partition key and sorted by sort key. You start by creating tables, no need to create or manage a DB. 

Tables capacity must be calculated and provision in advance. there is read capacity units RCU and write WCU. You can set up auto scaling and you also have burst credit for peak demand. When the credits expire you get the ProvisionThroughputException, in this case do exponential back off. 1 WCU = 1 write per second for item up to 1KB, if more than 1KB, one extra WCU per KB. In DynamoDB you can select between strong consistency read and eventual. By default is strong to get items but you can change it using ConsisentRead parameter. RCU = 1 strong read per second or 2 eventual per second for 4KB size. WCU and RCU are spread over partitions. If you exceed throuput you get the ProvisionThroughputException which may be caused by a hot partition, large items or hot keys. Solutions: use an evenly distributed key, back off, or use DynamoDB accelerator for read which is a cache. PutItem create or fully replace item. UpdateItem partial update of attributes. Conditional writes allow to write or read info only if a condition is true, this is good for concurrency since you can only replace a value if the original value is what you expected. There is also DeleteItem and DeleteTable. It is much efficient and cheaper to use batch: BatchWlriteItem up to 25 items for put or delete item. 16MB max batch, only one API call so less latency and AWS run the batch in parallel. Part of the batch can fail and is up to the client to retry. GetItem: read by key, uses eventual read by default. use ProjectionExpression to retrieve only some of the attributes. BatchGetItem: up to 100 items in parallel. Query returns values based on the key and sort key. You can define a filter as well but this is executed on the client. Up to 1MB of data returned and you can specify a limit. It is very efficient. Scan goes through the whole table and then fllters data which is not efficient, consumes a lot of RCU. You can use parallel scan for efficiency but lots of RCU. You can use Projection and Filter Expression. Scan is needed to see the whole table query needs equals in primary key so it will return just one item or group of items in case it is a primary + sort key. You can have up to 5 alternative local secondary indexes which are extra sort keys that must be defined when creating the table. There are also global secondary indexes to speed up queries on non keys attributes, the index is a new table that you can query and project values. GSI can be modified after table creation. So local secondary is to speed up queries of attributes inside a table that you are querying using the defined primary key and global indexes is to query primary keys that are not defined PKs, so you create new tables. DynamoDB is optimistic locking, you have conditional updates and deletes underr the hood using version numbers. 

DAX is DynamoDB accelerator, super performance read cache. When enabled writes go through DAX. It is multi AZ, up to 10 nodes and default TTL is 5 min. DynamoDB streams are a change log like kafka, every update, create and delete go to the stream. Lambda functions can subscribe to DynamoDB streams to react in real time to events. You can use the streams to replicate data across regions, the retention policy is 24h. DynamoDB supports VPC so you can access without internet and it is fully managed by IAM. You can have global tables across regions using streams as replication. There is a tool called DMS to import data from Mongo and other DBs. You can run it locally.



API Gateway is AWS api management tool to expose rest end points. Lambda + API gateway is serverless. It handles versioning of an API to support different versions for clients, authorization and authentication, different environments, swagger ad open api, key management and client throttling. It can also parse transform and validate request, it has a cache and also generates SDK and API specs. You need to make a deployment in the gateway for changes to take effect, you deploy to stages: dev, test, prod. You can have many stages and you have full history for rollback, each stage has env variables to set properties for each environment. This way you can change http end points and lambda functions (using context parameters). A common pattern is to use env variables to point to lambda aliases. API management support canary deployments. Mapping templates are used to modify in and out requests. You can parse the body, parameters, change content, add headers, map json to xml, etc. It uses VLT language.

Swagger is now a standard called Open API which AWS API gateway support. It can be written in yaml or json. You can export or import directly from AWS. Swagger can generate SDK for mobile apps. API gateway can use cache, default 5 min max 1h, clients with the right role can bypass cache using header: Cache-Controle:max-age=0.

For monitoring enable cloud watch at stage level. You have the request and response and many metrics, It also integrates with x ray. 

If you want to support calls from other rest services you need to enable CORS, in the console you can generate the OPTIONS call with the desired response. In API gateway you can define plans for different clients each one will have an API key, quota per stage and throttling settings. You define user plans first and then associate keys with them to reuse settings. For security create a IAM policy and assign it to a role, the gateway will apply permissions based on the a service called Sig v4 which attached credentials to requests headers. Lambda authorizers previously know as custom authorizers are used fro OAuth, SAML and any other 3rd party to validate credentials, it uses a cache. A lambda function is executed which return the policy for the given credentials. There is also cognito users pools for oauth. So, IAM is for users and apps within AWS, it handles authentication and authorization. Custom authorizer is for 3rd party tokens, very flexible and does auth plus authorization but you pay for lambda function call. Cognito is great for authentication using oauth google, facebook, etc. it does only authentication and you have to implement authorization.

Cognito is the authentication module for AWS. It has the Cognito User Pools (CUP) which is a serverless DB of user identities that can be simple(username and password) or federated using Oauh  like Facebook or Google; or SAML. It is based on JWT and integrated with API gateway which uses the JWT. There are also Federated Identity pools which are used to get temp access to AWS resources using identity providers. So you can login with facebook, get a token the request the federated pool for temp access to a S3 bucket if granted the client get this policy for a time period. This is for direct access while the user pool is for permanent using api gateway. Cognito Sync is deprecated for AppSync, it is used to store config, state and preferences of applications, it has cross device sync (android or IOs) and offline mode. It relies on federated pool.



SAM is the serverless application model. It is a complete framework for development and deployment of serverless apps. It uses SAM Yaml file that is used to generate complex cloud formation deployments. Only two commands to deploy to Prod and you can use CodeDeploy. With SAM you can run lambda, API gateway and DynamoDB locally. The SAM template is a yaml file that starts with Transform: AWS::Serverles. It has 3 core sections AWS::Serverless:Function for lambda, AWS::Serverless::api for API gateway and AWS::Serverless:::simple table for dynamo. To deploy you can use SAM package and deploy  or aws cloudformation package and deploy for cli.



KMS is AWS key management service which manages all the keys for data encryption. It is fully integrated with IAM. KMS is integrated with many services for encryption. You can also use the SDK and cli to encrypt and decrypt data. KMS manages your private key, it can rotate it for extra security, you do not need to worry about managing the key, you cannot even retrieve your own private key used for encryption, you can only ask KMS to encrypt data. The user master key is called CMK. So, you never store your secrets in plaintext, you ask KMS to encrypt them and then store them in env variables. It can only encrypt 4k data per call. For bigger use envelope encryption. 

To give access to KMS to a user make sure the key policy allows the user and that the IAM role allow the KMS API calls. KMS give us full key and policy management and cloud trail for audit. 

Three types of CMK, the default master which is free, you can create your own in KMS for 1$ a month or create your own and import it for 1$ month. There is also a charge per call to KMS. KMS is under IAM in the console under encryption keys. The key policy describes who can use the key and what they can do like update or delete. Encryption SDK is provided to do envelope encryption for data bigger than 4KB. This is different fro S3 encryption SDK. The API call to encrypt is GenerateDataKeyAPI.

AWS parameter store SSM is used to store secrets and configuration. It uses KMS and it is serverless so you don't have to do anything and you have a secure vault. There is a SDK and free, there is also version tracking to recover. The configuration management uses IAM, It integrates with cloud watch events  for notifications and cloudformation for deployments with secrets. So SSM is an easier alternative when you want to store parameters than using KMS directly. It uses a tree structure so you can define by app, then environment, etc. In the console is under EC2 or systems management. The parameters are based on paths so you can search by path: myapp/dev/dbpasswd. 

Cross account access: define a role in IAM for another account, define which accounts can access,  use AWS STS (secure token service) to get a token so the external account can assume the role using AssumeRole API, the access is between 15 min and 1h.



Cloud Front is an AWS CDN to add cache in the current 168 edge locations across regions, designed for S3 because a bucket can be created only in one region but also works for EC2. Can protect against DDos attacks and it has SSL termination but also can talk to your services using ssl. It support RTMP for video.

Step functions are used to create a state machine using a JSON file to orchestrate several lambda functions calls. There is also a designer. It integrates with EC2, ECS, api gateway.... You can have also human approval. It is used for workflows. 

SWF is similar to step functions but for EC2, not serverless, it is the simple workflow service. The manual intervention is better and supports parent and child processes, other than that AWS recommends step functions.



ECS is the container orchestration solution for AWS. There is also has EKS which is kubernetes whereas ECS is amazon specific Docker orchestration. The Core service runs containers on your user defined EC2 instances, simple: just runs Docker on linux EC2. Fargate is another solution to run tasks(pods) on containers on AWS managed instances, so it is serverless. EKS is Kubernetes managed by AWS, more portable. ECR is the docker registry managed by Amazon. ECS + ECR is great alternative to microservices if you don't use lambda. Lambda is more popular for green field and ECS to bring on prem services. Also ECS is popular for CI and batch. You create an ECS cluster on EC2 instances and define services which are replicated and call tasks(pods) which are running containers. Each EC2 can have multiple services and tasks, each container has integration with IAM for security. The new  ALB load balancer has integration with ECS for port mapping so you can replicate containers and assign dynamic ports so they can run on the same instance. This allows max utilization of cpu and ram and easier rolling updates. You need to run ECS agent with its config file on each EC2 instance. On EC2 Linux the agent is already installed but you still need to modify the ecs.config file. Main properties: ECS_CLUSTER, ECS_ENGINE_AUTH_DATA to authenticate to external repositories, ECS_AVAILABLE_LOGGING_DRIVERS to use cloud watch for logs, ECS_ENABLE_TASK_IAM_ROLE to enable role and policy check when running containers, very important, set it to true. ECR is the image repo fully integrated with IAM and secure. Code Build can build and push images to ECR.



SES is the simple email server. Integrated with IAM for security and with many services like S3 and Lambda. You can use SMTP or the SDK.

Redshift is the big data service for big queries, analytics and OLAP which is slow big data queries. This is the data warehouse and data lake solution. Neptune is the graph DB in AWS. DMS is the AWS sqoop equivalent, used to migrate data between RDS, DynamoDB and specially Redshift. There are other migration tools.