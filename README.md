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



lambda chnage names at:
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


