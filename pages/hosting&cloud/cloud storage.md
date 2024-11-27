# Table of Contents

## [AWS S3](#aws%20s3)
- [Create a Storage Service](#create%20a%20storage%20service)
- [Upload a File](#upload%20a%20file)
    - [Upload from the UI](#upload%20from%20the%20ui)
        - [Delete Files](#delete%20files)
    - [Upload with the CLI](#upload%20with%20the%20cli)
## [CloudFront](#cloudfront)
- [CDN](#cdn)
- [Upload to CloudFront](#upload%20to%20cloudfront)
## [Google Cloud CDN](#google%20cloud%20cdn)
- [CDN Overview](#cdn%20overview)
- [Create a Bucket](#create%20a%20bucket)
- [Upload Files to Bucket](#upload%20files%20to%20bucket)
- [Allow Public Access in Bucket Permissions](#allow%20public%20access%20in%20bucket%20permissions)
- [CDN Hosting](#cdn%20hosting)
## [Azure CDN](#azure%20cdn)
- [Install Azure CLI](#install%20azur%20cli)
- [Send File with CLI](#send%20file%20with%20cli)
- [Create a CDN](#create%20a%20cdn)
# aws s3
S3 allows to store files in a ***bucket***
## create a storage service
- create a bucket
- give a unique name
- leave everything to default except uncheck ``block all public access`` 
## upload a file
- edit bucket policy to allow all
from ``permissions`` tab
```javascript
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::BUCKET_NAME/*"
        }
    ]
}
```
### upload from the ui
- upload the file with `aws S3 console`
- get the `public url` of the object
#### delete files
- make sure to have `all access rights`
- `delete` objects by emptying bucket
### upload with the cli
[cli documentation](https://docs.aws.amazon.com/cli/latest/reference/s3/)
- upload images
```sh
aws s3 cp <source_dir> s3://<destination_bucket>/ --resursive # recursive for a directory
```
- check uploaded images
```sh
aws s3 ls s3://<destination-bucket>
```
- delete files
```sh
aws s3 rm s3://<destination-bucket>/ --recursive
```
# cloudfront
## cdn
CDN is a system of distributed servers strategically located around the world to deliver digital content (e.g., web pages, images, videos, scripts, stylesheets, APIs) to users quickly and efficiently. CDNs are designed to minimize latency, improve load times, and ensure content availability even during high traffic or server outages.
## upload to cloudfront
- cloudfront works with s3
- create an s3 bucket
bucket policy
```javascript
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<bucket-name>/*"
        }
    ]
}
```
- upload website resource
```sh
aws s3 cp ecw-website s3://<bucket-name>  --recursive
```
- create a ***distribution*** in cloudfront
	- add created s3 origin domain
	- redirect http to https
	- do not enable security protection (waf) for now
- check out the ``distribution domaine name`` + ``/index.html``
- delete everything:
	- empty s3 bucket
	- delete s3 bucket
	- disable cloudfront distribution
	- wait for last modified to have a datetime (instead of ``Deploying``)
# google cloud cdn
## [cdn overview](https://cloud.google.com/cdn/docs/overview)
## create a bucket
- create a unique name for the bucket
- leave default settings except unless untick: 
	- [ ] ``enforce public access prevention on this bucket`` for now
## upload files to bucket
- checkout [gcloud storage cli docs](https://cloud.google.com/sdk/gcloud/reference/storage)
```sh
gcloud storage cp ecw-website/ gs://mihamieat-lacapsule-bucket/ --recursive 
```
## allow public access in bucket permissions
- add allUsers in ``permissions`` > ``grant access``
## cdn hosting
- configure the bucket in order to activate static website hosting
	- go to ``buckets`` > find the bucket > ... > ``edit website configuration``
	- go to ``network services`` > ``cloud cdn`` > ``new origin`` 
		- create load balancer or add existing one
	- go to ``load balancer`` and get the ``frontend ip``/index.html
	- note: make sure that the source files are at the root of bucket.
- delete all
# azure cdn
- must create a ``storage account`` 
- create a container in ``blob service`` from created ``storage accound``
- allow ``blob anonymous access``
- change access level to ``blob (anonymous read access for blobs only)``
## install azur cli
[azure cli install doc](https://learn.microsoft.com/fr-fr/cli/azure/install-azure-cli)
```sh
az login
```
## send file with cli
[az storage docs](https://learn.microsoft.com/en-us/cli/azure/storage/azcopy/blob?view=azure-cli-latest#az-storage-azcopy-blob-upload)
```sh
az storage azcopy blob upload -c mihamieat-container --account-name mihamieat -s "ecw-website/" --recursive  
```
- also make sure that the files url is publicly available (check url on private browsing)
## create a cdn
- go to Front Door and CDN profiles