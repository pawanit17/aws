# AWS Hands-on

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
