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
{"key1":"hello:,
"key2": "9e",
"key3" : "m"}

