
https://github.com/pawanit17/aws#container-services-on-aws

# Table of contents
- [S3](https://github.com/pawanit17/aws#s3)
  - [Object vs Block Storage](https://github.com/pawanit17/aws#object-vs-block-storage--httpscloudnetappcomblogblock-storage-vs-object-storage-cloud-)
  - [Storage Classes](https://github.com/pawanit17/aws#storage-classes)
  - [Hosting a static website in AWS](https://github.com/pawanit17/aws#hosting-a-static-website-in-aws)
  - [S3 Versioning](https://github.com/pawanit17/aws#s3-versioning)
  - [S3 Replication](https://github.com/pawanit17/aws#s3-bucket-replication)
  - [S3 Locks](https://github.com/pawanit17/aws#locks)
  - [S3 Encryption](https://github.com/pawanit17/aws#encryption)
  - [S3 Performance](https://github.com/pawanit17/aws#s3-performance)
  - [S3 Summary](https://github.com/pawanit17/aws#s3-summary)
- [IAM](https://github.com/pawanit17/aws#iam)
- [EC2](https://github.com/pawanit17/aws#ec2)
  - [Load Balancer](https://github.com/pawanit17/aws#load-balancer)
    - [Application Load Balancer](https://github.com/pawanit17/aws#application-load-balancer)  
- [Serverless](https://github.com/pawanit17/aws#lambda--serverless)
  - [Lambda function that tells whether a web page is up or not](https://github.com/pawanit17/aws#hosting-a-lambda-function-that-tells-whether-a-web-page-is-up-or-not)
- [DynamoDB](https://github.com/pawanit17/aws#dynamodb)
- [Elastic Beanstalk](https://github.com/pawanit17/aws#elastic-beanstalk)
  - [Deploying a SpringBoot application to EBS](https://github.com/pawanit17/aws#deploying-a-springboot-jar-file-to-ebs)
- [CI/CD](https://github.com/pawanit17/aws#cicd)
  - [AWS CodeStar](https://github.com/pawanit17/aws#codestar)
- [Containers on AWS](https://github.com/pawanit17/aws#container-services-on-aws)
- [Knowledgeful Handson](https://github.com/pawanit17/aws#todo)
- [Answers](https://github.com/pawanit17/aws#answers)
  - [Deploying SpringBoot application on EBS](https://github.com/pawanit17/aws#deploying-a-springboot-application-to-elastic-beanstalk) 
  - [What services start when EBS service starts](https://github.com/pawanit17/aws#what-services-get-created-behind-the-scenes-when-ebs-service-starts-and-why-does-springboot-application-properties-has-to-be-updated-for-server-port)

# Introduction:
- Region is a location - Sydney, Capetown, Mumbai etc. Each Region contains 2 or more AZs.
- Availability Zone is like a datacenter - Hitech Campus Eindhoven. This can be more than one datacenter. Each AZ in a region are like 100Kms from each other.
- Edge Location - Endpoints for caching like CloudFront (CDN). More than 200 edge locations.

- Whitepapers: https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html?did=wp_card&trk=wp_card

![image](https://user-images.githubusercontent.com/42272776/160228124-a09bbc41-1c93-4495-b23b-ac73e4637375.png)

# Questions
- How do you deploy a full stack application to AWS.
- How does the application connect to the database.
- *How are REST APIs exposed to outside world.
- *What are VPCs.
- What are Roles, IAM, security groups.
- 🏃 How are logs of an application viewed in AWS
- Deploy a NodeJS application to EC2 and EBS
- 👍 Deploy a SpringBoot application to EBS
- *How are docker based applications deployed to AWS
- Ecs service
- Where does K8s come into picture for AWS
- Build a simple application that uploads file to S3
- 👍 Build a simple application on SpringBoot and deploy to AWS using Elastic Beanstalk
- 👍 Build a simple application with a front end that communicates to AWS backend on EBS.
- 🏃 Build an app that retuns a list of movies of a given genre.
- *Build an app that leverages AWS load balancer
  - Application load balancer 
- Build a simple application on SpringBoot and deploy it to containers and then to AWS using containers
- CI/CD of a simple application
- How to connect to an Elastic Beanstalk server using SSH or RDP?.


# List
- Storage
  - S3
- Database
  - DynamoDB
  - ElasticCache
  - Amazon Keyspaces
  - RDS
- Servers
  - EC2
  - Elastic Beanstalk
  - Lambda
- Containers
  - Elastic Container Registry
  - Elastic Container Service
  - Elastic Kubernetes Service
- Deploying applications
- Logging / Monitoring
- Networking
  - VPC
  - Route 53
  - API Gateway 
- CI/CD
  - CodeCommit
  - CodeBuild
  - CodeDeploy
  - CodePipeline

# Services

| Category | Service      | Description |
| ----------- | ----------- | ----------- |
| Storage | S3      | Simpe Storage Service. S3 offer 99.999999999 durability and 99 availability. It also offers various Storage classes.  Data is automatically distributed across minimum of three physical Availability Zones within the AWS region. https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html https://aws.amazon.com/s3/pricing/    |
| Serverless | Lambda   | Serverless        |
| Logging | Cloud Watch | Application and Infrastructure Monitoring https://aws.amazon.com/cloudwatch/ |
| CICD | CodeCommit | AWS CodeCommit is a secure, highly scalable, managed source control service that hosts private Git repositories. |
| CICD | CodePipeline | Automated tests and deployment into environments when the source code changes |
| CICD | CodeBuild | Fully manage service that compiles, tests and builds the deliverables for deployment |
| CICD | CodeDeploy | Automates code deployments to any instances |
| CICD | CodeStar | Used to create pipelines using the above 4 services as a wrapper |

# Overview
## S3
- S3 is **object** based storages - Image, text, webpage. So can't be used as a database. S3 scales on demand.
- **Unlimited** storage. Object max size is **5TB**.
- S3 **buckets** are like **folders** in S3 - Finance, HR etc, but need to have **Universal** Unique name.
- URL for the bucket looks like: https://bucket-name.s3.Region.aws.com/key-name
- When we upload an object to a bucket, each object would have the below information:
- **Key** for the objects is typically the name of the objects.
- **Value** is the actual content made up of sequence of bytes.
- **Metadata** is the actual metadata associated with the objects ( last accessed, content type etc ).
- **Version ID** To identify multiple versions of the objects.
- S3 Standard is the default version.
- High Availability 99.99%
- High Durability 99.999999999%
- Frequent access
- CDN, Mobile Apps, Big Data are applications.
- **Lifecycle Management** is the scheme for moving data that meets a certain threshold to move to cheaper S3 options like glacier/deep glacier.
- **Bucket Policies** work at **Bucket level** and specify what actions are allowed or denied at bucket level. Ex: PUT are allowed but not DELETE.
- **ACL**s work at individual **object level** and define which AWS accounts are granted access and they type of access. The ACLs can be attached on individual objects within a bucket as well.
- Strong Read-After-Write Consistency.
### Object vs Block Storage ( https://cloud.netapp.com/blog/block-storage-vs-object-storage-cloud )
  - Object storage is useful for data that does not change often. Write-once Ready-Many times usecases. Also this is compatible with distributed systems - data stored in multiple nodes.
  - Block storage is useful for holding databases/caches. Also for high intensive IO operations.
  - Searches are fast with Object storage. Big Data analytics usecases.
  - Updates with Block storage are easier as we have access to individual blocks. With object storage, this is not possible. Entire file has to be created again.
  - S3 offers Object storage. Amazon Elastic Block Storage offers Block storage solutions.
- https://aws.amazon.com/s3/faqs/
- Is a storage service with high durability and availability and can hold files/objects and host a static website, serve as an archive of data.
- Various storage classes exist that have varying cost implications.
- Different storage classes have different replication behavior.
- Can encrypt data using security keys.
- Lifecycle policy helps in moving data between storage classes, purging after a certain threshold etc.
- Replication policy helps in copying the data to a different location / region to help in minimising the access times.
- Individual objects within the S3 bucket can be shared for public access while the bucket itself is private.
- Selected objects can be specifically shared in an S3 bucket while the bucket itself is not shared. ![image](https://user-images.githubusercontent.com/42272776/146680953-97ba6781-3d8d-4d09-a5f6-993f3dc04ff8.png)

### Storage classes
- S3 has different storage classes that are used based on the frequency of access.
- ![image](https://user-images.githubusercontent.com/42272776/146633171-52a6d85b-10ff-4f5f-a9c2-532a1677a051.png)
- ![image](https://user-images.githubusercontent.com/42272776/146680782-11e8a8f1-a325-4032-9caa-02873018633f.png)
- Archive feature is related to S3 Glacier / S3 Deep Archive Glacier.
- ![image](https://user-images.githubusercontent.com/42272776/160279856-14d956c0-e282-4c78-b09f-212a16e2519e.png)
- ![image](https://user-images.githubusercontent.com/42272776/160279897-62f4c204-a3a1-40cb-809c-7aa94eb39833.png)

### Hosting a static website in AWS
![image](https://user-images.githubusercontent.com/42272776/143780612-5294497e-e81d-41df-b878-bc8caa2896c4.png)
- Bucket Policy determines who all can use/access the bucket/its content.
- /* means making the Policy applicable to all the objects in the Bucket.
- We create an S3 bucket and upload the error.html and index.html files in it.
![image](https://user-images.githubusercontent.com/42272776/143780919-490da1e0-ff37-4d4c-a22f-05d0ae0b4537.png)
- We then update the policy for this bucket in its Permissions section.
![image](https://user-images.githubusercontent.com/42272776/143780927-5bd655fc-c9e4-4acf-8f7a-5aefbe35ad7b.png)
- We also configure the Static website hosting in bucket Properties.
![image](https://user-images.githubusercontent.com/42272776/143780943-bd7fba54-5e44-4afd-b00b-ebcff8f288df.png)
![image](https://user-images.githubusercontent.com/42272776/143780793-fc175b66-8ebe-4781-a2c1-e9a34e445dff.png)

### S3 Versioning
- **Versioning** can be configured at **Bucket level** so that when a file with same name is uploaded, a new version gets created.
- Versioning cannot be disabled, only suspended.
- Policies do not apply to the previous versions of the objects in the bucket. Explicit access needs to be granted via Make Public action.
- Deleting an object that has versioning turned on, will create a Delete marker instead. If this marker is deleted, then the objects are available again. 
- ![image](https://user-images.githubusercontent.com/42272776/144109147-b74bae10-32b6-4200-ae6a-23a8fc4a579c.png)
- Unlimited number of versions can be created. https://acloud.guru/forums/aws-csa-2019/discussion/-LzddK__zQps2CcoZum9/How%20many%20versions%20of%20a%20file%20can%20be%20saved%20in%20S3%3F
- ![image](https://user-images.githubusercontent.com/42272776/144108361-71753a72-9fae-4bdb-b3d3-78b46fa94be1.png)
- Public access can be granted from the UI of AWS on the Bucket/Object. But with a Bucket Policy, better control is provided statements/principals/actions/resources.
```
{
    "Version": "2012-10-17",
    "Id": "unique-id-to-describe-below-statement",
    "Statement": [
        {
            "Sid": "unique-sid",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::testbucket99912121/*"
        }
    ]
}
```

### S3 Bucket Replication
![image](https://user-images.githubusercontent.com/42272776/143920852-223d5357-00c9-4d9d-8b81-0e395fa5dac4.png)
- Create Bucket 1 and Bucket 2
- In Management of Bucket 1, create a **Replication Rule** with Source as Bucket 1 and Target as Bucket 2.
- ![image](https://user-images.githubusercontent.com/42272776/143920961-555fe1ae-7fd2-489b-a64b-1d21c583e140.png)
- Any new files that are updated to AWS in Bucket 1 will now sync to Bucket 2 automatically.
- ❓ How to sync existing ones?.

### S3 Bucket with Versioning and Deletion Protection - Lifecycle Configuration
- ![image](https://user-images.githubusercontent.com/42272776/146632881-a7023323-7325-4b9b-b412-559e206a72f2.png)
- Objects that are stored in S3 buckets may need to be deleted or moved to a different less costly storage after some time. Further, there may be certain objects in an S3 bucket that are to be archived. All these are configured using a Lifecycle rule.
- Lifecycle configuration also applies to versions of the objects.
- By defauly, Delete markers are not replicated. This could be turned on though.
- A note on encryption. https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-encryption.html
- ![image](https://user-images.githubusercontent.com/42272776/146633227-65ac3655-b4a1-40b3-9e78-d0004e356db0.png)
- ![image](https://user-images.githubusercontent.com/42272776/146632986-33cbb68f-53d6-492e-a213-93609edeff4b.png)
- ![image](https://user-images.githubusercontent.com/42272776/146633002-a59f973b-dc3d-4925-88dc-3d28959067cf.png)
- ![image](https://user-images.githubusercontent.com/42272776/146633012-936a34f0-9892-4e10-9e9a-cf6d57c417a7.png)

### Locks
- Object locks are of two types - Governance and Compliance.
- They determine whether an update to an object is possible or not.
- Compliance Mode - An Object cannot be overwritten or deleted by any user, including the root user.
- Governance Mode - An Object cannot be overwritten or deleted by a user, unless that user has special permissions.

### Encryption
- Encryption in Transit
  - HTTPS
  - SSL/TLS
- Encryption at Rest: Server side Encryption
  - SSE-S3: S3 managed keys, using AES 256 (x-amz-server-side-encryption:AES256)
  - SSE-KMS: AWS KMS managed keys (x-amz-server-side-encryption:aaws:kms)(limites to upload and download)
  - SSE-C: Customer provided keys
- Encryption at Rest: Client side Encryption
  - Encrypt of files yourself before upload to S3
- S3 bucket policy can be introduced to stop the upload of files for the PUT requests that do not have x-amz-server-side-encryption flag.

### S3 Performance
- Using prefixes help in the performance of READs
- Prefix is nothing but the hierarchy. For ex: mybucketname/folder1/subfolder1/myfile.jpg.
- You can achieve better performance if the prefixes are more.
- Your applications can easily achieve thousands of transactions per second in request performance when uploading and retrieving storage from Amazon S3. Amazon S3 automatically scales to high request rates. For example, your application can achieve at least 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second per prefix in a bucket. There are no limits to the number of prefixes in a bucket. You can increase your read or write performance by parallelizing reads. For example, if you create 10 prefixes in an Amazon S3 bucket to parallelize reads, you could scale your read performance to 55,000 read requests per second. Similarly, you can scale write operations by writing to multiple prefixes.
- Multipart uploads are used to upload larger files in S3 efficiently ( better to use for > 100MB and definitely > 5GB ).
- Use S3 byte range fetches to increase performance when downloading files to S3.
- When using KMS, there is an upper limit. Breaching this would slower performance.

### S3 Summary
- S3 is Simple Storage Service - highly available and durable.
- A static web hosting option is possible.
- Making a bucket and its content public can be done via a JSON policy.
- Is Object based storage and so is suitable for write-once and read-many times scenario.
- Not suitable as a database or cache.
- Storage classes decide the ease of retrieval and costs involved.
- Can configure replication rules to move data between regions, lifecycle rule to move data between different storage classes.
- Different versions of the same object could also live, which are configured by versioning rules.
- Encryption is supported - client side and server side.
- Prefixes to names help in increased performance.

## IAM
- Root Account - Has full administrative account for the AWS account.
- Multi Factor Authentication configuration lets you secure the root account.
- Alternative options are creating an admin group for administrators and assigning the appropriate permissions to this group followed by creating user accounts to these administrators.
- Policies
  - Access is controlled via policy documents, which are JSON documents.
  - Ex: Allow the ability to do everything with every resource - user or group to which this policy is applied to.
 ```
 {
   "Version": "2012-10-17",
   "Statement": [
     {
       "Effect": "Allow",
       "Action": "*",
       "Resource": "*"
     }
   ]
}
```
![image](https://user-images.githubusercontent.com/42272776/160850792-85530990-f796-40e6-b51e-f46ac9bb906a.png)
- In general, for ease of maintenance, policies are not applied to Users. Instead they are applied at Group level and Users are added to those groups.
- Users, Groups, Policies are Global.
- **Building Blocks**
  - Users(Physical person)
  - Groups(Functions such as Adminstrator, Developer)
  - Roles(internal use in AWS, allows one part of AWS to access another part of AWS).
- Principle of least privilege
  - Give minimum privilege and add more privilege as per need.
  - When a new user is created, by default he does not have any access.
- SAML - To use the same username and password that a user uses to log into Windows, to log onto AWS. IAM Federation.

## EC2
- Elastic Compute Cloud
- Types of instances
  - On Demand
    - Pay be the hour or second. 
  - Reserved
    - Reserve the capacity for 1-3 years. 
  - Spot Instances
    - Buy unused instances at cheaper prices. Good for applications that have flexible start and end times. 
  - Dedicated
    - Banking, Finance applications could have certain regulations to not deploy in multi tenancy virtualization.
- EC2 instances need VPC for operation.


## Load Balancer
- A brief intro to the differences between these two services.
- Application Load Balancer
  - The listeners work at layer 7 and have access to request headers.
  - URL based, Host based, Query String based load balancing.
  - This is suited for Microservices based applications as this service can load balance Containers as well.
  - Works with Http, Https, gRPC protocols.  
- Network Load Balancer
  - Operates at Network level.
  - TLS offloading can be done at Network Load Balancer.
  - Suited for cases where Low latency is expected.
  - UDP, TCP, TLS protocols apply here.
- Both the load balancing services are newer generation.
- Classic load balancer are deprecated.

### Application Load Balancer
- We designate a group of EC2 instances as a target group and an Application Load Balancer service is configured to bound this target group.
- ![image](https://user-images.githubusercontent.com/42272776/166507445-0be41fc2-d1cf-4660-8c07-e24405ded8eb.png)
- We can even configure sticky sessions in the target group - which may be useful for stateful applications.
- Two EC2 instances for which an ALB shall be configured
- ![image](https://user-images.githubusercontent.com/42272776/166507004-ee31bd6b-0b87-484d-897c-6073080efbcb.png)
- Target group looks like below
- ![image](https://user-images.githubusercontent.com/42272776/166507951-30b12054-3826-47ea-8d41-28a609c1217b.png)

# Lambda / Serverless

Lambda
- [Hosting a Lambda function to determine if a Web Page is Up or Not](#hosting-a-lambda-function-that-tells-whether-a-web-page-is-up-or-not)
- 
## Hosting a Lambda function that tells whether a web page is up or not
![image](https://user-images.githubusercontent.com/42272776/143782240-0956fddd-d006-489d-abf1-779e19bb6eb6.png)
- Execution role is like the service account that is used to run the lambda function.
- Create an AWS Lambda Function with NodeJS as the language.
![image](https://user-images.githubusercontent.com/42272776/143782396-0fe12395-962d-41ef-b7fa-3bd625a52d26.png)
![image](https://user-images.githubusercontent.com/42272776/143782138-6965ea3e-6388-4c5a-b2bd-73d206d9848c.png)
- The logging information from a Lambda function gets routed to AWS cloud watch.
- Notice the time billed for the operation.
- Custom logging information also goes to AWS Cloud Watch - console.xxx statements.
![image](https://user-images.githubusercontent.com/42272776/143782116-fbedd5de-a894-4826-b65b-33d655bfb703.png)
- For reference: https://docs.aws.amazon.com/lambda/latest/dg/nodejs-logging.html

# DynamoDB

# Elastic Beanstalk
## Deploying a SpringBoot jar file to EBS
- A simple SpringBoot application that processes GET, POST, DELETE and PUT requests onto the URI /movies.
```
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("movies")
public class RestAPIController {

    @GetMapping
    public String getUser() {
        return "Get Movies";
    }

    @PostMapping
    public String createUser() {
        return "Post Movies";
    }

    @PutMapping
    public String updateUser() {
        return "Put Movies";
    }

    @DeleteMapping
    public String deleteUser() {
        return "Delete Movies";
    }
}
```
- ![image](https://user-images.githubusercontent.com/42272776/146810781-0c15c93a-af37-4c16-8278-82b1fe4736c2.png)
- Good read: https://cloudkatha.com/how-to-deploy-spring-boot-application-to-aws-elastic-beanstalk/
- Set up an environmental variable SERVER_PORT with value 5000.
- ![image](https://user-images.githubusercontent.com/42272776/146811707-a94055d6-fb67-421f-b333-595ae3abf061.png)
- ![image](https://user-images.githubusercontent.com/42272776/146812011-9ce235ac-0c4e-4d6a-9cf1-1bb02e720215.png)

# CI/CD

## CodeStar
- AWS had a new service release in 2017, called CodeStar.
- It is a fully managed service and encapsulates the other CI/CD services.
- We have to choose a template in CodeStar and it would create the other services as shown below based on our selection.
- ![image](https://user-images.githubusercontent.com/42272776/145706729-41e96a0e-e6bd-403e-906b-f8c313f83f54.png)
- CodeStart also provisions CodeCommit repository for the project and an update to the content in that repository triggers a CI/CD pipeline.
- ![image](https://user-images.githubusercontent.com/42272776/145706814-7c7943a3-2276-44b0-98e1-52bd2d1a39a6.png)
- ![image](https://user-images.githubusercontent.com/42272776/145706701-64096930-e719-4be0-8e32-b74bf5a37941.png)

## CodeCommit

## Container services on AWS
- Fargate
- ECS
  - Elastic Cloud Service
Read on: 
https://towardsdatascience.com/deploying-a-docker-container-with-ecs-and-fargate-7b0cbc9cd608
- EKS
- ECR
- Copilot?

## Messaging Services
### Simple Notification Server - SNS
- What problem does message queues solve?
  - Tight coupling: If the two systems are directly connected, a message cannot be sent to the second system if it is down.
  - Performance: The producer can produce as many messages as they would want and the consumer would only process them at its own pace. 
- Fully managed service with auto scailng.
- Encryption at rest is automatically provided. For encryption in transit, developers need to create key/value pairs and manually do the configuration.
- Composed of Topics ( think of it as an event type or a subject ) and Subscriptions to those Topics.
  - App to App { SQS }
  - App to Person { Email, SMS } 
- SNS employs a Pub-Sub model.
- It is a notification service. Useful when more than one system is to be notified.
- SNS can send notifications to SQS which can then be used by the target application for instance.
- SNS vs SQS
  - If other systems need to know about an event generated, use SNS.
  - If only the current system cares about it, use SQS.
  - SNS is a PUSH system. SQS is a PULL system.

```
- One SQL can broadcast messages to several SQL using SNS.
- SQS -> SNS -> SQS1
             -> SQS2
             -> SQS3
```

- Sample usecase
![image](https://user-images.githubusercontent.com/42272776/171029813-66c43f71-acf7-46e6-ae27-b45dea2e49ed.png)
- A number of users may be subscribed to promotion offers form retail chains, they are notified via these pub-sub architectures.
- Connecting Lambda with SNS has one disadvantage that if the lambda processing fails, the message gets lost.
- SNS can be integrated with HTTP endpoints, Emails, SMS messages.

- Options
  - We can configure who can send messages to SNS.
  - Delivery retry policy.
  - Logging facility @ CloudWatch.
  - Filter Policy determines who among the subscribers should be sent the message.
  - Message Attributes can be created that help in realizing Filter Policy.
    - Ex: purchaseType -> Internet.
  - Dead Letter Queue - Temp Queue that contains messages which could not be sent to the receiver.
  - Push notifications are supported by SNS. 

#### SpringBoot on AWS - Subscribing and Receiving Notification
![IMG_20220530_231108197](https://user-images.githubusercontent.com/42272776/171040670-f94c3bf4-9061-4b2b-9116-06a4211a6b4b.jpg)
- One REST API endpoint does a GET Request to Subscribe an email address to an SNS topic.
- Another REST API endpoint does a GET REQUEST to publish the content to SNS topic. This action would make the SNS service to send the email/notification to all the subscriber i.e., first point.
- https://www.youtube.com/watch?v=lF7Ba4-8ER4

```
@Configuration
public class AWSSNSConfig {

    @Primary
    @Bean
    public AmazonSNSClient getSnsClient(){
        return (AmazonSNSClient) AmazonSNSClientBuilder.standard().withRegion(Regions.US_EAST_1)
                .withCredentials(new AWSStaticCredentialsProvider(new BasicAWSCredentials("AKIA2TKUBX7JOPEJLYUV","PHmuqdARP+hgQ/A9qtAKQuNHyC2lptycfoTQwgx4")))
                .build();
    }
}
```

```
@SpringBootApplication (exclude = {ContextStackAutoConfiguration.class, ContextRegionProviderAutoConfiguration.class})
@RestController
public class SnsConnectorApplication {

	@Autowired
	private AmazonSNSClient snsClient;

	String TOPIC_ARN="arn:aws:sns:us-east-1:728710102994:hello-queue-topic";

	@GetMapping("/subscribe/{email}")
	public String subscribe(@PathVariable String email) {

		SubscribeRequest request = new SubscribeRequest(TOPIC_ARN, "email", email);
		snsClient.subscribe(request);

		return "Programmatic subscription is pending. Check email!" + email;
	}

	@GetMapping("/publish")
	public String publish(){

		PublishRequest request = new PublishRequest(TOPIC_ARN, "Testing on-going", "Notification: Hello!!");
		snsClient.publish(request);
		return "Programmatic Notification send successfully";
	}


	public static void main(String[] args) {
		SpringApplication.run(SnsConnectorApplication.class, args);
	}

}
```

# TODO
| URL      | Description |
| ----------- | ----------- |
|https://learn.acloud.guru/handson/d524d389-9ee2-490a-9f2d-95e0502b3682|Creating a DynamoDB Table|
|https://learn.acloud.guru/handson/aacf9e92-0bb7-4969-aaf7-e2e106a7e339|Deploy an Amazon RDS Multi-AZ and Read Replica in AWS|
|https://learn.acloud.guru/handson/e43cb83b-29db-4387-ae52-16d148d8445b|Create and Work with an EC2 Instance in AWS|
|https://learn.acloud.guru/handson/d901786a-b8a6-404c-9fc2-d55cf103f5ff|Use Application Load Balancers for Web Servers|
|https://learn.acloud.guru/handson/98627abc-6348-4ac3-8c66-e03e76dfbf5a|AWS DynamoDB in the Console - Creating Tables, Items, and Indexes|
|https://learn.acloud.guru/handson/30295528-e932-4241-86fe-b8acaaba6c72|Programmatically Utilizing Data From S3|
|https://learn.acloud.guru/handson/87f886fa-a4d2-4fa4-b9d6-e15faa744ded|Setting Up a Pipeline with a Manual Approval in AWS CodePipeline|
|https://learn.acloud.guru/handson/f0626640-3d35-4dd8-9a9c-2f90dfd9f1de|Working with a DevOps CI/CD Pipeline in AWS using CodeStar |
|https://learn.acloud.guru/handson/7eaff9b2-dd90-48cd-9675-dfb8f62c8a09|Implement Advanced CloudWatch Monitoring for a Web Server|
|https://learn.acloud.guru/handson/cbda1fbf-6c65-439c-b284-ed96ef0e1f9d|Querying Data in S3 with Amazon Athena|
|https://learn.acloud.guru/handson/d8590da1-be72-4e06-8a31-2e6e1c9863b6|Configuring S3 Buckets for Versioning and Deletion Protection |
|https://learn.acloud.guru/handson/a0c93cdb-127d-43e5-9026-aea0a8dc5c5d|Creating and Configuring a Network Load Balancer in AWS|
|https://learn.acloud.guru/handson/3f2be21a-91fd-4872-aa33-58a1ee38e832|Migrating from a Relational Database to DynamoDB|
|https://learn.acloud.guru/handson/41b87a5a-b7e9-45d3-bd7c-cf9d93557a01|Joining, Enriching, and Transforming Streaming Data With Amazon Kinesis|
|https://learn.acloud.guru/handson/b3dd0d1c-b4cf-489f-8a5b-fd0ccbf6d8fd|Creating an AWS CodeCommit Repository That Triggers Email Notifications|
|https://learn.acloud.guru/handson/aae676dc-fe12-4fff-8d16-dd6a25e12f2b|Building a Serverless Application Using Step Functions, API Gateway, Lambda, and S3 in AWS|
|https://learn.acloud.guru/handson/2d9e37e1-3733-4227-8e46-8d22dc519585|Configuring Amazon S3 Buckets to Host a Static Website with a Custom Domain|
|https://learn.acloud.guru/handson/d70cdd62-361e-4dc9-af83-30a6b1ba4db5|Implementing an Elasticsearch Backed Search Microservice|
|https://learn.acloud.guru/handson/d524d389-9ee2-490a-9f2d-95e0502b3682|Creating a DynamoDB Table|
|https://learn.acloud.guru/handson/f2b58b6b-2a05-435a-8746-ca1ff25b9773|Creating a Simple AWS Lambda Function|
|https://learn.acloud.guru/handson/682d1793-2bc5-455b-9485-97be5499b676|Creating a Basic Lambda Function to Shut Down an EC2 Instance|
|https://learn.acloud.guru/handson/ab9e8bda-1f6f-4af8-9465-f8e3e14cc7d1|Building a Microservice Application and DynamoDB Data Model|
|https://learn.acloud.guru/handson/61adc9c0-7327-4212-bb45-372d61db939f|Using a DynamoDB Table Basic I/O|
|https://learn.acloud.guru/handson/349a802d-49b3-41a1-8cbe-d211c05d4133|CodePipeline for Continuous Deployment to Elastic Beanstalk|
|https://learn.acloud.guru/handson/4b94c76a-7cab-4f50-accc-3709552dfdd7|Securing Your S3 Bucket from A to Z|
|https://learn.acloud.guru/handson/9c11732b-b9f7-403d-8cb8-d70f7b5f34fb|Using Data Pipeline to Export DynamoDB Data to S3|
|https://learn.acloud.guru/handson/9f1588c0-7186-475b-8bd1-9d88b86779e5|Querying Data in Amazon S3 with Amazon Athena|
|https://learn.acloud.guru/handson/262a58ab-49e1-4102-b2a2-b746c06ba74d|Working with AWS SQS FIFO Queues|
|https://learn.acloud.guru/handson/8a6fba26-ff01-457a-98db-8524a69bae65|Deploying a Highly Available Web Application and a Bastion Host in AWS|
|https://learn.acloud.guru/handson/2319a3d1-8ece-4352-8636-212cca0f0c9d|Using CloudWatch Dashboards to Monitor Resource Utilization|
|https://learn.acloud.guru/handson/1167a5fe-7953-4f6c-89ed-50e8b18ccac3|Creating and Subscribing to AWS SNS Topics|
|https://learn.acloud.guru/handson/c89bb3e8-4974-4168-be3b-ffe292824608|Assigning a FQDN (Fully Qualified Domain Name) to an EC2 Instance Using Route 53|
|https://learn.acloud.guru/handson/bef560af-6b54-4d0f-a95d-b941ec44cfb3|Deploying to AWS with Terraform and Ansible|
|https://learn.acloud.guru/handson/28d93bf2-b21d-4e5d-b351-4dc83d9f1070|Implementing a Simple DynamoDB Application|
|https://learn.acloud.guru/handson/593008ac-cae1-477e-a13e-51099eadb042|Processing DynamoDB Streams Using Lambda|
|https://learn.acloud.guru/handson/4690c366-3c29-4b6d-8014-0f837d5a54e5|Building a CI/CD Pipeline with AWS CodePipeline to Deploy a Static Website on S3|
|https://learn.acloud.guru/handson/4d3da1ac-fae1-4f00-bf07-c11b20a2e2ad|Deploying to AWS with Ansible|
|https://learn.acloud.guru/handson/38c6212e-1a0e-4e04-ad09-5ec0e2efe3e1|Manipulating EC2 Instances with Ansible|
|https://learn.acloud.guru/handson/45429a7c-d00e-4887-a7e4-4b42a5f4d1cc|Deploying and Updating a Web Application with a CI/CD Pipeline Using AWS CodeStar|
|https://learn.acloud.guru/handson/ad821099-977c-4b46-9eec-b60ef6aa37d7|Deploying a Website Canary with CloudFormation|
|https://learn.acloud.guru/handson/16697a70-25bf-4fc5-a110-ff907a5393c9|Using Prometheus with Kubernetes|
|https://learn.acloud.guru/handson/f978617e-40a2-4174-8ea4-5e29be5dea90|Deploying to AWS with Travis CI|
|https://learn.acloud.guru/handson/4030bdd4-e7a1-470c-84d3-22d6b0fc4bca|Scaling a MEAN App in Lightsail Using App Tiers|
|https://learn.acloud.guru/handson/711879e3-75f6-417e-a6eb-f72e1b561c35|Introduction to Amazon S3|

- Udemy
https://wipro.udemy.com/course/deploy-java-spring-apps-online/

# Answers

## Deploying a SpringBoot application to Elastic Beanstalk
- Develop a SpringBoot application and build the jar for it using mvn install.
- Application.properties has to be configured with server.port=5000 to facilitate Nginx reverse proxy.
- In AWS, under EBS, create a service uploading this jar as the payload.
![image](https://user-images.githubusercontent.com/42272776/166973958-cacb2c83-91d6-42ad-aec3-7ef6a62f60af.png)
- Once the service starts, the application can be accessed.
![image](https://user-images.githubusercontent.com/42272776/166973630-d6c0d8db-4f6e-4b7d-a37f-cc1e9b747df0.png)

## What services get created behind the scenes when EBS service starts and why does SpringBoot application properties has to be updated for server port?.
- When an EBS service starts, it also starts an **Elastic load balancer**, an **Nginx proxy**, atleast **one EC2 instance**, **Security Groups**, **IP Addresses** behind the scenes.
- https://pragmaticintegrator.wordpress.com/2016/07/12/run-your-spring-boot-application-on-aws-using-elastic-beanstalk/
- Nginx forwards the requests to destination server on port 5000 by default. This is why this setting is needed.
![image](https://user-images.githubusercontent.com/42272776/166974797-9d71e2c7-0a64-4cf6-b2ed-434342840046.png)

