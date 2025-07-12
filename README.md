sns in topi edit access policy paste this

{
    "Version": "2012-10-17",
    "Id": "example-ID",
    "Statement": [
        {
            "Sid": "Example SNS topic policy",
            "Effect": "Allow",
            "Principal": {
                "Service": "s3.amazonaws.com"
            },
            "Action": [
                "SNS:Publish"
            ],
            "Resource": "arn:aws:sns:us-east-1:456482669069:mytopic58K",
            "Condition": {
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:s3:::snsbucket58k"
                },
                "StringEquals": {
                    "aws:SourceAccount": "456482669069"
                }
            }
        }
    ]
}





sqs:


console.log("Loading function");

export const handler = async (event, context) => {
    for (const record of event.Records) {
        const messageBody = record.body;
        console.log("Raw message body:", messageBody);

        try {
            const data = JSON.parse(messageBody);
            console.log('value1 =', data.key1);
            console.log('value2 =', data.key2);
            console.log('value3 =', data.key3);
        } catch (err) {
            console.error("Error parsing message body:", err);
        }
    }

    return "SQS message(s) processed";
};


in msg body: 
{"key1":"hello":,
"key2": "9e",
"key3" : "m"}




i am role commands:
1-> TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
2-> curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/iam/info
3-> curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/iam/security-credentials/
4-> aws s3api create-bucket --bucket 59e-bucket1mumbai --region ap-south-1 --create-bucket-configuration LocationConstraint=ap-south-1
5-> aws s3 ls



lambda chnage names at in lambda exp:
dynamoTable = dynamodb.Table('YourDynamoDBTableName')


vpc bootstarp script

#!/bin/bash
sudo su
yum update -y
yum install httpd -y
cd /var/www/html
echo "22BD1A059E" > index.html
service httpd start
chkconfig httpd on


pem putty commands
12. enter following commands:
->sudo yum update -y
->sudo yum install httpd -y
->sudo systemctl status http 

->sudo systemctl start httpd
->sudo systemctl enable httpd
13. go back to instace select it copy public ipv4 addess you can see the msg as it works!

nginx commands:
EXP-3: EC2 with Ubuntu                     => try again with pem
1. everything is same just choose AMI as ubuntu
2.Run following commands:
->sudo apt-get update -y
->sudo apt install docker.io
->sudo docker pull nginx
->sudo docker run -d -p 80:80 --name mynginx nginx    ->ones check it works or not
-> sudo docker exec -it mynginx bash
cd /usr/share/nginx/html
ls yo get index.html
   -> apt update
   -> apt install nano
   -> nano index.html change h1 content ctrl+O and ctrl+X
   -> exit
3.copy ipv4  if ot owrks try wuth :80

CRR
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

VPC:
create VPC => 10.0.0.0/16
public subnet => select vpc , 10.0.1.0/24
pvt subnet => select vpc 10.0.2.0/24
internet gateway => create and attach to VPC
route table-1 => create , edit route add IGW 

ebs

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

