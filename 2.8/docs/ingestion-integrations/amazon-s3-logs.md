---
type: page
title: AWS S3
listed: true
slug: amazon-s3-logs
description: Use Mezmo to collect all the logs your AWS services send to S3, and then send them to Mezmo.
index_title: AWS S3
hidden: 
keywords: 
tags: 
---





The Mezmo Amazon S3 integration uses [AWS Lambda](https://docs.aws.amazon.com/lambda/index.html) to process and transform your log data as it is retrieved from [S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/Welcome.html), and then routes your logs from S3 to Mezmo. Using our Mezmo integration, you can configure a Lambda function to subscribe to your AWS S3 bucket and then optionally use environment variables to fine-tune the function.

For more detailed information about the Mezmo AWS Lambda function, refer to the documentation in our public [GitHub repository](https://github.com/logdna/logdna-s3/tree/v2.0.0).



