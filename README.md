# AWS Hands-on

S3
- [Hosting a Static Website](#hosting-a-static-website-in-aws)
- [Bucket Versioning](#s3-versioning)
- [Bucket Replication](#s3-bucket-replication)

Lambda
- [Hosting a Lambda function to determine if a Web Page is Up or Not](#hosting-a-lambda-function-that-tells-whether-a-web-page-is-up-or-not)

## Services

| Service      | Description |
| ----------- | ----------- |
| S3      | Simpe Storage Service. S3 offer 99.999999999 durability and 99 availability. It also offers various Storage classes.  https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html https://aws.amazon.com/s3/pricing/    |
| Lambda   | Serverless        |
| Cloud Watch | Logging |


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
https://learn.acloud.guru/handson/d524d389-9ee2-490a-9f2d-95e0502b3682



# TODO
https://learn.acloud.guru/handson/aacf9e92-0bb7-4969-aaf7-e2e106a7e339
https://learn.acloud.guru/handson/e43cb83b-29db-4387-ae52-16d148d8445b
https://learn.acloud.guru/handson/d901786a-b8a6-404c-9fc2-d55cf103f5ff
https://learn.acloud.guru/handson/98627abc-6348-4ac3-8c66-e03e76dfbf5a
https://learn.acloud.guru/handson/30295528-e932-4241-86fe-b8acaaba6c72
https://learn.acloud.guru/handson/87f886fa-a4d2-4fa4-b9d6-e15faa744ded
https://learn.acloud.guru/handson/f0626640-3d35-4dd8-9a9c-2f90dfd9f1de
https://learn.acloud.guru/handson/7eaff9b2-dd90-48cd-9675-dfb8f62c8a09
https://learn.acloud.guru/handson/cbda1fbf-6c65-439c-b284-ed96ef0e1f9d
https://learn.acloud.guru/handson/d8590da1-be72-4e06-8a31-2e6e1c9863b6
https://learn.acloud.guru/handson/a0c93cdb-127d-43e5-9026-aea0a8dc5c5d

