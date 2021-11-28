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
