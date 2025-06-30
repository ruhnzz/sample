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

