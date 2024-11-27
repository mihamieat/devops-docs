- provides access to technology services : compute power, storage, databases.
- resources are available on demand.
- pay for what you use.
## S3
- ***S3 buckets*** suitable for static webpage.
- Store ***any type*** or ***amount*** of data and retrieve it from ***anywhere***.
- Any type of file and any metadata is called an ***object***.
- Objects are stored in S3 containers called ***buckets***.
- ***Fully managed*** service: no need to deploy or manage any server.
- ***Automatically replicated*** across multiple AWS datacenters for ***high resiliency***.
- Can scale to *handle* thousands of *requests*.
- For others to access the S3 bucket, ***permissions*** must be configured to allow that access. A ***bucket policy*** can be created to configure these permissions.
- A bucket policy, written in Json format, defines ***who can access the bucket*** and ***what type of operations*** can be performed.
## EC2
- Elastice Compute Cloud
- Web service that provides reliable, scalable, ***compute capacity*** in the cloud.
- Can launch virtual server in minutes.
- To help improve server resilience: use AWS infrastructure to place  EC2s into two different ***Availability Zones***.
- AZ: ***logical datacenter*** in an AWS Region that has redundant ans *separate* power, networking and connectivity. Each AZ is supported by one or more physical datacenters.
- 