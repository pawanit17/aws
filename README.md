# Introduction:
- Region is a location - Sydney, Capetown, Mumbai etc. Each Region contains 2 or more AZs.
- Availability Zone is like a datacenter - Hitech Campus Eindhoven. This can be more than one datacenter. Each AZ in a region are like 100Kms from each other.
- Edge Location - Endpoints for caching like CloudFront (CDN). More than 200 edge locations.

- Whitepapers: https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html?did=wp_card&trk=wp_card

![image](https://user-images.githubusercontent.com/42272776/160228124-a09bbc41-1c93-4495-b23b-ac73e4637375.png)

# Questions
- How do you deploy a full stack application to AWS.
- How does the application connect to the database.
- How are REST APIs exposed to outside world.
- What are VPCs.
- What are Roles, IAM, security groups.
- 🏃 How are logs of an application viewed in AWS
- Deploy a NodeJS application to EC2 and EBS
- Deploy a SpringBoot application to EC2 and EBS
- How are docker based applications deployed to AWS
- Where does K8s come into picture for AWS
- Build a simple application that uploads file to S3
- 👍 Build a simple application on SpringBoot and deploy to AWS using Elastic Beanstalk
- 👍 Build a simple application with a front end that communicates to AWS backend on EBS.
- 🏃 Build an app that retuns a list of movies of a given genre.
- Build an app that leverages AWS load balancer
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

# Summary
S3
- Is a storage service with high durability and availability and can hold files/objects and host a static website, serve as an archive of data.
- Various storage classes exist that have varying cost implications.
- Different storage classes have different replication behavior.
- Can encrypt data using security keys.
- Lifecycle policy helps in moving data between storage classes, purging after a certain threshold etc.
- Replication policy helps in copying the data to a different location / region to help in minimising the access times.
- Individual objects within the S3 bucket can be shared for public access while the bucket itself is private.

- [Hosting a Static Website](#hosting-a-static-website-in-aws)
- [Bucket Versioning](#s3-versioning)
- [Bucket Replication](#s3-bucket-replication)


Lambda
- [Hosting a Lambda function to determine if a Web Page is Up or Not](#hosting-a-lambda-function-that-tells-whether-a-web-page-is-up-or-not)


# S3
- S3 is object based storages - Image, text, webpage. So can't be used as a database.
- Unlimited storage. Object max size is 5TB.
- S3 buckets are like folders in S3 - Finance, HR etc, but need to have Universal Unique space.
- Object vs Block Storage
  - Object storage is useful for data that does not change often. Write-once Ready-Many times usecases. Also this is compatible with distributed systems - data stored in multiple nodes.
  - Block storage is useful for holding databases/caches. Also for high intensive IO operations.
  - Searches are fast with Object storage. Big Data analytics usecases.
  - Updates with Block storage are easier as we have access to individual blocks. With object storage, this is not possible. Entire file has to be created again.
  - S3 offers Object storage. Amazon Elastic Block Storage offers Block storage solutions.
- https://aws.amazon.com/s3/faqs/
- S3 has different storage classes that are used based on the frequency of access.
- ![image](https://user-images.githubusercontent.com/42272776/146633171-52a6d85b-10ff-4f5f-a9c2-532a1677a051.png)
- ![image](https://user-images.githubusercontent.com/42272776/146680782-11e8a8f1-a325-4032-9caa-02873018633f.png)
- Selected objects can be specifically shared in an S3 bucket while the bucket itself is not shared. ![image](https://user-images.githubusercontent.com/42272776/146680953-97ba6781-3d8d-4d09-a5f6-993f3dc04ff8.png)

## Hosting a static website in AWS
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

## S3 Versioning
- Versioning can be configured at Bucket level so that when a file with same name is uploaded, a version gets created.
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

## S3 Bucket Replication
![image](https://user-images.githubusercontent.com/42272776/143920852-223d5357-00c9-4d9d-8b81-0e395fa5dac4.png)
- Create Bucket 1 and Bucket 2
- In Management of Bucket 1, create a Replication Rule with Source as Bucket 1 and Target as Bucket 2.
- ![image](https://user-images.githubusercontent.com/42272776/143920961-555fe1ae-7fd2-489b-a64b-1d21c583e140.png)
- Any new files that are updated to AWS in Bucket 1 will now sync to Bucket 2 automatically.
- ❓ How to sync existing ones?.

## S3 Bucket with Versioning and Deletion Protection - Lifecycle Configuration
- ![image](https://user-images.githubusercontent.com/42272776/146632881-a7023323-7325-4b9b-b412-559e206a72f2.png)
- Objects that are stored in S3 buckets may need to be deleted or moved to a different less costly storage after some time. Further, there may be certain objects in an S3 bucket that are to be archived. All these are configured using a Lifecycle rule.
- A note on encryption. https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-encryption.html
- ![image](https://user-images.githubusercontent.com/42272776/146633227-65ac3655-b4a1-40b3-9e78-d0004e356db0.png)
- ![image](https://user-images.githubusercontent.com/42272776/146632986-33cbb68f-53d6-492e-a213-93609edeff4b.png)
- ![image](https://user-images.githubusercontent.com/42272776/146633002-a59f973b-dc3d-4925-88dc-3d28959067cf.png)
- ![image](https://user-images.githubusercontent.com/42272776/146633012-936a34f0-9892-4e10-9e9a-cf6d57c417a7.png)

# Lambda / Serverless
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

# TODO
| HandsOn Description      | Status |
| ----------- | ----------- |
|https://learn.acloud.guru/handson/d524d389-9ee2-490a-9f2d-95e0502b3682||
|https://learn.acloud.guru/handson/aacf9e92-0bb7-4969-aaf7-e2e106a7e339||
|https://learn.acloud.guru/handson/e43cb83b-29db-4387-ae52-16d148d8445b||
|https://learn.acloud.guru/handson/d901786a-b8a6-404c-9fc2-d55cf103f5ff||
|https://learn.acloud.guru/handson/98627abc-6348-4ac3-8c66-e03e76dfbf5a||
|https://learn.acloud.guru/handson/30295528-e932-4241-86fe-b8acaaba6c72||
|https://learn.acloud.guru/handson/87f886fa-a4d2-4fa4-b9d6-e15faa744ded||
|https://learn.acloud.guru/handson/f0626640-3d35-4dd8-9a9c-2f90dfd9f1de|Working with a DevOps CI/CD Pipeline in AWS using CodeStar |
|https://learn.acloud.guru/handson/7eaff9b2-dd90-48cd-9675-dfb8f62c8a09||
|https://learn.acloud.guru/handson/cbda1fbf-6c65-439c-b284-ed96ef0e1f9d||
|https://learn.acloud.guru/handson/d8590da1-be72-4e06-8a31-2e6e1c9863b6| Configuring S3 Buckets for Versioning and Deletion Protection |
|https://learn.acloud.guru/handson/a0c93cdb-127d-43e5-9026-aea0a8dc5c5d||
|https://learn.acloud.guru/handson/3f2be21a-91fd-4872-aa33-58a1ee38e832||
|https://learn.acloud.guru/handson/41b87a5a-b7e9-45d3-bd7c-cf9d93557a01||
|https://learn.acloud.guru/handson/b3dd0d1c-b4cf-489f-8a5b-fd0ccbf6d8fd||
|https://learn.acloud.guru/handson/aae676dc-fe12-4fff-8d16-dd6a25e12f2b||
|https://learn.acloud.guru/handson/2d9e37e1-3733-4227-8e46-8d22dc519585||
|https://learn.acloud.guru/handson/d70cdd62-361e-4dc9-af83-30a6b1ba4db5||
|https://learn.acloud.guru/handson/d524d389-9ee2-490a-9f2d-95e0502b3682||
|https://learn.acloud.guru/handson/f2b58b6b-2a05-435a-8746-ca1ff25b9773||
|https://learn.acloud.guru/handson/682d1793-2bc5-455b-9485-97be5499b676||
|https://learn.acloud.guru/handson/ab9e8bda-1f6f-4af8-9465-f8e3e14cc7d1||
|https://learn.acloud.guru/handson/61adc9c0-7327-4212-bb45-372d61db939f||
|https://learn.acloud.guru/handson/349a802d-49b3-41a1-8cbe-d211c05d4133||
|https://learn.acloud.guru/handson/4b94c76a-7cab-4f50-accc-3709552dfdd7||
|https://learn.acloud.guru/handson/9c11732b-b9f7-403d-8cb8-d70f7b5f34fb||
|https://learn.acloud.guru/handson/9f1588c0-7186-475b-8bd1-9d88b86779e5||
|https://learn.acloud.guru/handson/262a58ab-49e1-4102-b2a2-b746c06ba74d||
|https://learn.acloud.guru/handson/8a6fba26-ff01-457a-98db-8524a69bae65||
|https://learn.acloud.guru/handson/2319a3d1-8ece-4352-8636-212cca0f0c9d||
|https://learn.acloud.guru/handson/1167a5fe-7953-4f6c-89ed-50e8b18ccac3||
|https://learn.acloud.guru/handson/c89bb3e8-4974-4168-be3b-ffe292824608||
|https://learn.acloud.guru/handson/bef560af-6b54-4d0f-a95d-b941ec44cfb3||
|https://learn.acloud.guru/handson/28d93bf2-b21d-4e5d-b351-4dc83d9f1070||
|https://learn.acloud.guru/handson/593008ac-cae1-477e-a13e-51099eadb042||
|https://learn.acloud.guru/handson/4690c366-3c29-4b6d-8014-0f837d5a54e5||
|https://learn.acloud.guru/handson/4d3da1ac-fae1-4f00-bf07-c11b20a2e2ad||
|https://learn.acloud.guru/handson/38c6212e-1a0e-4e04-ad09-5ec0e2efe3e1||
|https://learn.acloud.guru/handson/45429a7c-d00e-4887-a7e4-4b42a5f4d1cc||
|https://learn.acloud.guru/handson/ad821099-977c-4b46-9eec-b60ef6aa37d7||
|https://learn.acloud.guru/handson/16697a70-25bf-4fc5-a110-ff907a5393c9||
|https://learn.acloud.guru/handson/f978617e-40a2-4174-8ea4-5e29be5dea90||
|https://learn.acloud.guru/handson/4030bdd4-e7a1-470c-84d3-22d6b0fc4bca||
|https://learn.acloud.guru/handson/711879e3-75f6-417e-a6eb-f72e1b561c35|Introduction to Amazon S3|

- Udemy
https://wipro.udemy.com/course/deploy-java-spring-apps-online/
