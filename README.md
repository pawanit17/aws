# Questions
- How do you deploy a full stack application to AWS.
- How does the application connect to the database.
- How are REST APIs exposed to outside world.
- What are VPCs.
- What are Roles, IAM.
- How are logs of an application viewed in AWS
- Deploy a NodeJS application to EC2 and EBS
- Deploy a SpringBoot application to EC2 and EBS
- How are docker based applications deployed to AWS
- Where does K8s come into picture for AWS
- CI/CD of a simple application

# List
- Storage
- Database
- Servers
- Deploying applications
- Serverless
- Logging / Monitoring
- VPC and Networking
- CI/CD

# Services

| Category | Service      | Description |
| ----------- | ----------- | ----------- |
| Storage | S3      | Simpe Storage Service. S3 offer 99.999999999 durability and 99 availability. It also offers various Storage classes.  https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html https://aws.amazon.com/s3/pricing/    |
| Serverless | Lambda   | Serverless        |
| Logging | Cloud Watch | Logging |
| CICD | CodeCommit | AWS CodeCommit is a secure, highly scalable, managed source control service that hosts private Git repositories. |
| CICD | CodePipeline | Automated tests and deployment into environments when the source code changes |
| CICD | CodeBuild | Fully manage service that compiles, tests and builds the deliverables for deployment |
| CICD | CodeDeploy | Automates code deployments to any instances |
| CICD | CodeStar | Used to create pipelines using the above 4 services as a wrapper |



# AWS Hands-on

S3
- [Hosting a Static Website](#hosting-a-static-website-in-aws)
- [Bucket Versioning](#s3-versioning)
- [Bucket Replication](#s3-bucket-replication)

Lambda
- [Hosting a Lambda function to determine if a Web Page is Up or Not](#hosting-a-lambda-function-that-tells-whether-a-web-page-is-up-or-not)


# S3
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


# CI/CD
- AWS had a new service release in 2017, called CodeStar.
- It is a fully managed service and encapsulates the other CI/CD services.
- We have to choose a template in CodeStar and it would create the other services as shown below based on our selection.
- ![image](https://user-images.githubusercontent.com/42272776/145706729-41e96a0e-e6bd-403e-906b-f8c313f83f54.png)
- CodeStart also provisions CodeCommit repository for the project and an update to the content in that repository triggers a CI/CD pipeline.
- ![image](https://user-images.githubusercontent.com/42272776/145706814-7c7943a3-2276-44b0-98e1-52bd2d1a39a6.png)
- ![image](https://user-images.githubusercontent.com/42272776/145706701-64096930-e719-4be0-8e32-b74bf5a37941.png)


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
|https://learn.acloud.guru/handson/d8590da1-be72-4e06-8a31-2e6e1c9863b6||
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
|https://learn.acloud.guru/handson/711879e3-75f6-417e-a6eb-f72e1b561c35||
