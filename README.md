Cloud Computing:

WEEK-1

EXP-1: EC2 WITH PEM , Amazon linux

1.login into your aws academy account
2.start aws lab and go all services->compute->ec2
3.click on launch instance
4.give the name to instance
5.select amazon machine image which is template for software configuration which contains os like Linux,ubutu, windows select amazon linux
6.let the instance type be t2 micro which comes with 1 cpu and 1gb 
7.create a key pair of .pem 
8.in network setting allow all the traffic of ssh,httpand https 
9.let everything else be at default click on launch instance
10. then the instance will be successfully get created selct on it and click on connect and go to ssh client copy the ssh command
11. navigate to folder where we save the .pem open cmd and paste ssh command 
12. enter following commands:
->sudo yum update -y
->sudo yum install httpd -y
->sudo systemctl status http 

->sudo systemctl start httpd
->sudo systemctl enable httpd
13. go back to instace select it copy public ipv4 addess you can see the msg as it works!

EXP-2: EC2 WITH PUTTY, Amazon linux

1. everything is similar at key pair select .ppk then launch instace
2.select instance go to ssh client copy the commnad from ec2
3.now open putty paste it here then in left panel select SSH->Auth->Credentials click on browse and select the .ppk file click on open
4. click on accept the putty terminal will open
5. enter following commands as previous
6. copy paste the public ipv4


EXP-3: EC2 with Ubuntu

1. everything is same just choose AMI as ubuntu
2.Run following commands:
->sudo apt-get update -y
->sudo apt install docker.io
->sudo docker pull nginx
->sudo docker run --name mynginx -d -p 8080:80 nginx
-> sudo docker exec -it mynginx /bin/sh = bash
cd /usr/share/nginx/html
ls yo get index.html
   -> apt-get update
   -> apt-get upgrade //optional
   -> apt-get install nano
   -> nano index.htmledit in h1 wirte rollno
   -> exit
3.copy ipv4 with port :8080  

---------------------------------------------------------------------------------------------------------------------------------------------

                                         WEEK-2
EXP-1: S3-BUCKET CREATION:

1.login into your aws academy account
2.start aws lab and go all services->storage->S3
3.click on create bucket
4.give the globally unique name to bucket 
5.let everything be at default conditions click on create bucket
5. now select the bucket go to object tab and click on upload
6. click on add files and add the file you want to store in the bucket
7. copy the object url into browser you get the msg as access denied this is because we didn't enable the object level and bucket level permisions
Bucket Level Permissions
8. select bucket and go to permissions tab and scroll to bucket public access and click on edit 
9.uncheck all the options and acknowledge  it
10. scroll down to object ownership click on edit 
11.enable acl and click on save changes
12. now you in acl click on edit and in everyone check the List and read
Object Level Permissions
13. selct the object added to bucket go to  permissions tab 
14. go acl click on edit and in everyone check List and read
15. now copy pate the object url


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

                                      WEEK - 3
EXP-1 : S3 -VERSIONING AND RECOVERY

Bucket Versioning: is a feature in cloud storage services (like AWS S3, Google Cloud Storage, or Azure Blob Storage) that helps track changes to objects within a bucket by maintaining multiple versions of those objects.
The Two Main Functions of Bucket Versioning:
1.	Maintaining Versions of Objects:
●	  When you update an object, instead of replacing the existing file, a new version is created while the older versions are retained.
●	  Each version has a unique version ID, which allows you to retrieve any previous version if needed.
●	This helps in tracking changes, auditing modifications, and restoring data to an earlier state.
2.	Recovering Deleted Objects:
●	 If an object is deleted, the system does not permanently erase it; instead, it marks the latest version as a "delete marker."
●	Older versions remain intact, meaning you can recover accidentally deleted objects by restoring a previous version.
●	This prevents data loss due to accidental deletions and adds an extra layer of protection.


1.login into your aws academy account
2.start aws lab and go all services->storage->S3
3.click on create bucket and create two buckets bucket1 with versioning and bucket2 without versioning
4.give the globally unique name to buckets
5. in bucket1 enable the bucket versioning
6. and Let everything be at default in both buckets and click on create 

Recovery of Objects
7. Now upload the same object into both the buckets
8. Now delete the uploaded objects from both buckets while deleting in object in bucket with versioning it ask confirmation by typing delete and in bucket without versioning it will ask confirmation by typing permanently delete
9. Now in bucket with versioning you can see the toggle called show versions enable it you can see the file you deleted as delete marker 
10.delete the delete marker it will ask confirmation by typing permanently delete then disable the toggle you can see the file is recovered back
11. which is not possible in the bucket without versioning

Versioning 
12.Add same file into two buckets
13. again add the same file into two buckets where the files will be replaced new added file with current time stamp 
14. In he bucket with versioning when you enable the toggle called show versions you can see the previous version of file is also stored you can identify them by timestamp here the it will create the new object and maintains the previous version too
15 . which is not seen in the bucket without versioning because here it replaces the object


EXP-2 : STATIC WEB HOSTING:

●Static web hosting is a type of web hosting where only static files (HTML, CSS, JavaScript, images, etc.) are served directly to users without server-side processing. Unlike dynamic websites, which rely on databases and backend scripting (like PHP, Node.js, or Python), static websites consist of pre-built content that remains the same for every user until manually updated.

1.login into your aws academy account
2.start aws lab and go all services->storage->S3
3.click on create bucket
4.give the globally unique name to bucket let everything be at default click on create bucket
5. now upload the object click on upload->add files then upload 
6. make sure you enable the bucket level(bucket public access-uncheck, object ownership - enable then ACL in everyone check List and Read and object level permissions(ACL in everyone check List and Read)
7. then go to properties tab scroll down to Static web hosting click on edit and enable it
8. under it in index document enter the filename as portfolio.html clik on save changes and copy the static url
9. paste the url in browser you can see the file
10.now delete the object and reload the static url you can see the massage as 404 Not Found
11. now upload the another object error.html
12. Make sure to enable the object level permissions to newly added object
13. go to properties tab scroll down to Static web hosting and click on edit in index document under portfolio.html enter error.html click on save changes which will open if portfolio.html is not available
14. now reload the static url you can see the error.html page


EXP-3 : CROSS REGION REPLICATION

●	 If you want objects uploaded to a source bucket to be automatically reflected in a destination bucket, you need to set up S3 Replication.
1.	Cross-Region Replication (CRR) → If the destination bucket is in a different AWS region.
2.	Same-Region Replication (SRR) → If the destination bucket is in the same AWS region.

1.login into your aws academy account
2.start aws lab and go all services->storage->S3
3.click on create bucket
5. create two buckets source bucket in North Virginia and destination bucket in Oregano 
4.give the globally unique name to buckets enable the versioning for both buckets and rest everything be at default click on create bucket
5. select the source bucket go to management tab scroll down to replication rules and click on create replication rule
6. enter replication rule name
7. under source select apply to all objects in the bucket 
8. under destination click on s3 browse and select the destination bucket and click on choose path
9. Under IAM role choose LabRole
10. under additional replication options check Replication Time control click on save 
11. then check Yes and click on submit
12. you will led to tab called create batch operations job
13. under completion report select all tasks and click on browse s3 select destination bucket
14. under Permissions select IAM role as LabRole click on save
15. now upload object in source bucket then go to destination bucket you find the object which was uploaded in source bucket

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
                                                           WEEK -4                                                                                                                            

EXP-1:       

1.create instance with instance type as t2.nano

volume creation
2.go to volumes click on create volumes
3. create volume wuth size:20gb and avialbility zone same has instance

Volume attach
4.select the volume created click actions->attach volume
5.select the created instance and device name as /dev/sdf click attach volume   

mount the volume and resize
6.connect to ec2 instance and run following commands
->sudo su
->lsblk =>list of attached disks
-> fdisk -l
-> lsblk -fs (xvdb)
->fdisk /dev/xvdf
-> m n p 1 2times enter then w
-> partprobe
-> lsblk -fs
->mkfs.xfs /dev/xvdf1
->lsblk -fs
-> mkdir /mnt/cse9e
->mount /dev/xvdf1 /mnt/cse9e
->lsblk -fs
->cd /mnt/cse9e
->touch file {1..10}
-> ls -l
****************************
->sudo yum install git -y
go to git hub and get url of java maven project
-> git clone link
->ls
*****************************8
-> vi /etc/fstab
 I enter /dev/xvdb1 /mnt/cse9e xfs default 0 0 enter esc :wq
   
->cd /mnt/cse9e
->ls

Unmount:
->umount /mnt/cse
->cd /mnt/cse9e
->ls

again vi /etc/fstab I remove esc :wq

7.select volume go to action->detach volume

Now create a new instance and attach this volume to that instance
->sudo su
->lsblk -> dec/xvdf or b
->lsblk -fs
-.mkdir /mnt/cse
->mount /dev/xvdf1 /mnt/cse
->cd /mnt/cse
->ls

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------                 
                                                                         WEEK -5

exp-1 Snapshot:

1. create a ec2 instance ebs in N.virginia
2. create a volume with 20gb in availability zone of ebs 
3.click on create volume
4.select created volume and actions->attach volume
5. select the instance ebs and device name as /dev/xvdf
6. go instance and get connected execute following commands
->sudo su
->lsblk
->mkfs.xfs /dev/xvdf 
->mkdir /mnt/cse
->mount /dev/xvdf /mnt/cse
->cd /mnt/cse
->yum install git -y
-> git clone https://github.com/ruhnzz/javaMavenProject.git
->ls

create sanpshot
7.go to volumes select the volume we created actions->create snapshot
8.give name to snapshot click on create snapshot
9.go to snapshots you can see snapshot is created

create instance in Oregano 
10.create instance as ebsoregano in oregano
11.go to snapshot select it click action->copy snapshot 
12.give name and destination as oregano (us-west-2) click on copy snapshot
13.agian select the snapshot actions->create volume from snapshot
14.size will be same as 2 g just give availability zone of ebsOregano then create volume
15.select newly created volume and attach it to ebsOregano select device name as /dev/xvf
16.go to ebsOregano instance and connect to it
17.execute following commands
->sudo su
->lsblk
->mkdir /mnt/ce
->mount /dev/xvdf /mnt/cse
->cd /mnt/cse
->ls

exp-2 : EFS

1.create two instances with ppk and default vpc and different subnets of different availability zones and create security group EFS-MID then ssh and nfs protolcol
2.now connect instances with putty
3. Run following commands
->sudo su
->mkdir efs
->yum update -y
->yum install -y amazon-efs-utils
4.searh efs and create file system enter file name select default vpc click on create 
5.click on file system we created scroll to network tab click on manage and assign the security groups EFS-MID to availability zones where the instances are created
6.now click on attach copy the mount line
7. if inactive restart sudo su copy paste the line both terrminals the cd efs for both
8. 1st-> touch f1 int 2nd ls you will f1 here 



-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 
                                                                      WEEK -6:

exp-1 :vpc

Region
mathematica
Copy
Edit
Region: US East (N. Virginia)
✅ Step 1: Create a VPC
vbnet
Copy
Edit
Name: 58z-VPC1
CIDR: 10.0.0.0/16
Tenancy: Default
✅ Step 2: Create Subnets
Public Subnet (WebServer + Bastion)

vbnet
Copy
Edit
Name: 58z-WebServer
CIDR: 10.0.1.0/24
AZ: us-east-1a
Auto-assign public IP: Enabled ✅
Private Subnet (DBServer)

vbnet
Copy
Edit
Name: 58z-DbServer
CIDR: 10.0.2.0/24
AZ: us-east-1b
Auto-assign public IP: Disabled ❌
✅ Step 3: Internet Gateway
vbnet
Copy
Edit
Create: 58z-IGW1
Attach to: 58z-VPC1
✅ Step 4: Route Tables
Public Route Table

makefile
Copy
Edit
Name: 58z-RT1
Associate: 58z-WebServer
Route: 0.0.0.0/0 → Internet Gateway (58z-IGW1)
Private Route Table (To be created later when NAT is available)

✅ Step 5: Launch EC2 Instances
Web Server
Subnet: 10.0.1.0/24

Key Pair: webKP30.pem

SG Inbound:

nginx
Copy
Edit
SSH → My IP
HTTP → Anywhere
DB Server (Private)
Subnet: 10.0.2.0/24

Key Pair: dbKP30.pem

SG Inbound:

nginx
Copy
Edit
MYSQL → Source: 10.0.1.0/24
Bastion Server
Subnet: 10.0.1.0/24

Key Pair: Bastion30.pem

SG Inbound:

nginx
Copy
Edit
SSH → My IP
✅ Step 6: Transfer DB Key to Bastion (No WinSCP)
From your local terminal, run:

bash
Copy
Edit
scp -i Bastion30.pem dbKP30.pem ec2-user@<Bastion-Public-IP>:/home/ec2-user/
✅ Step 7: SSH Access
From Local to Bastion:
bash
Copy
Edit
ssh -i Bastion30.pem ec2-user@<Bastion-Public-IP>
From Bastion to Private DB:
bash
Copy
Edit
chmod 400 dbKP30.pem
ssh -i dbKP30.pem ec2-user@<Private-DB-Private-IP>
❌ Step 8: Git Fails in Private DB (No Internet)
bash
Copy
Edit
sudo yum install git -y
# Fails due to no outbound internet access
✅ Step 9: Add NAT Gateway
Allocate Elastic IP

Create NAT Gateway in Public Subnet

Route Table: 58z-RT2

Route: 0.0.0.0/0 → NAT Gateway

Associate to Subnet: 58z-DbServer

✅ Step 10: Final Verification
bash
Copy
Edit
# On private DB (through Bastion)
sudo yum install git -y
git --version
✅ Now your private EC2 instance has internet access via the NAT Gateway, and you connected to it without using WinSCP.

