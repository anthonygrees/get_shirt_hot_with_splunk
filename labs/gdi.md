# GDI - Get Data In to Splunk from AWS
  
[Back to the Lab Index](../README.md#get-shirt-hot-with-splunk)
  
### About
There are so many different AWS services and logs that can be sent to Splunk.  With most customer having multiple AWS accounts and organisations it is important to configure the way you bring your data in using automation.  The main reasons to use automation is:  
- it uses code to define your configurations.  
- it is a pattern that can be used to configure 1, 2, 3 or 50 AWS accounts.  
- it ensures each environment is configured identically and in a consitent way.  
- it is `code` so you can version control it and collaborate on it.    
  
![GDI](/images/gdi/gdi.png)
  
  
### Your Options
There are a number of automated options to configure the way data is sent into your Splunk environment.  Here are some details on the following methods:  
- Terraform.  
- Trumpet.  
- Splunk Observability (SignalFX method).  
  
  
#### 1. Terraform
Terraform modules can be used to configure a Kinesis Firehose, set up a subscription for a desired CloudWatch Log Group to the Firehose, and send the log data to Splunk. A Lambda function is required to transform the CloudWatch Log data from "CloudWatch compressed format" to a format compatible with Splunk.  
  
For Example.  
```bash
resource "aws_kinesis_stream" "kinesis_stream" {
  name             = "tf-${var.app_name}-kinesis-stream"
  shard_count      = "${var.shard_count}"
  retention_period = "${var.retention_period}"

  shard_level_metrics = "${var.shard_level_metrics}"

  tags = {
    owner = "${var.app_name}"
  }
}
```
  
A great example of this is the repo created by Disney that you can view [here](https://github.com/disney/terraform-aws-kinesis-firehose-splunk).  
  
For more generic details on using Terraform to configure Kinesis you can read [this](https://github.com/easyawslearn/terraform-aws-kinesis).
  
  
#### 2. Trumpet
![Trumpet](https://github.com/splunk/splunk-aws-project-trumpet/blob/master/README-static-assets/trumpet_logo.png)   
Trumpet is a tool that leverages AWS CloudFormation to set up all the AWS infrastructure needed to push AWS CloudTrail, AWS Config, and AWS GuardDuty data to Splunk using HTTP Event Collector (HEC).  
  
The GitHub project for Trumpet is [here](https://github.com/splunk/splunk-aws-project-trumpet).
  
You can fill in this online form and generate the CloudFormation code. [Link](https://splunktrumpet.github.io/)
  
#### 3. Splunk Observability
Configure the Amazon Web Services (AWS) integration to connect your AWS account to Observability Cloud. When you configure the integration, you can import metrics and logs from supported AWS services. The integration uses Amazon CloudWatch Metrics and Logs to export data to Observability Cloud.  
  
Configuring CloudWatch Metric Streams delivery to Splunk Observability Cloud involves the following steps:  
1. Use the AWS integration wizard to integrate AWS with Splunk Observability Cloud.  
2. Add Metric Streams actions and permissions to the default AWS IAM policy.  
3. Define roles and permissions in AWS to enable streaming metrics.  
4. Create an Amazon Kinesis Data Firehouse Stream to receive AWS CloudWatch Metrics and a AWS S3 Bucket to store any records that fail delivery for retry.  
5. Use AWS CloudWatch to send metrics to an AWS Kinesis Stream.  
6. Configure AWS Kinesis Stream to forward metrics to Splunk Infrastructure Monitoring.  
7. Use the Splunk Infrastructure Monitoring API to set the `metricStreamsSyncState` field to `ENABLED`.  
  
The policy below gives permissions to collect data from every supported AWS service. If you plan to collect data from only a subset of AWS services that Observability Cloud supports, you can modify the `Action` and `Resource` fields.  
  
```json
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Effect": "Allow",
   "Action": [
    "apigateway:GET",
    "autoscaling:DescribeAutoScalingGroups",
    "cloudfront:GetDistributionConfig",
    "cloudfront:ListDistributions",
    "cloudfront:ListTagsForResource",
    "cloudwatch:DescribeAlarms",
    "cloudwatch:GetMetricData",
    "cloudwatch:GetMetricStatistics",
    "cloudwatch:ListMetrics",
    "dynamodb:DescribeTable",
    "dynamodb:ListTables",
    "dynamodb:ListTagsOfResource",
    "ec2:DescribeInstances",
    "ec2:DescribeInstanceStatus",
    "ec2:DescribeRegions",
    "ec2:DescribeReservedInstances",
    "ec2:DescribeReservedInstancesModifications",
    "ec2:DescribeTags",
    "ec2:DescribeVolumes",
    "ecs:DescribeClusters",
    "ecs:DescribeServices",
    "ecs:DescribeTasks",
    "ecs:ListClusters",
    "ecs:ListServices",
    "ecs:ListTagsForResource",
    "ecs:ListTaskDefinitions",
    "ecs:ListTasks",
    "elasticache:DescribeCacheClusters",
    "elasticloadbalancing:DescribeLoadBalancerAttributes",
    "elasticloadbalancing:DescribeLoadBalancers",
    "elasticloadbalancing:DescribeTags",
    "elasticloadbalancing:DescribeTargetGroups",
    "elasticmapreduce:DescribeCluster",
    "elasticmapreduce:ListClusters",
    "es:DescribeElasticsearchDomain",
    "es:ListDomainNames",
    "kinesis:DescribeStream",
    "kinesis:ListShards",
    "kinesis:ListStreams",
    "kinesis:ListTagsForStream",
    "lambda:GetAlias",
    "lambda:ListFunctions",
    "lambda:ListTags",
    "logs:DeleteSubscriptionFilter",
    "logs:DescribeLogGroups",
    "logs:DescribeSubscriptionFilters",
    "logs:PutSubscriptionFilter",
    "organizations:DescribeOrganization",
    "rds:DescribeDBInstances",
    "rds:ListTagsForResource",
    "redshift:DescribeClusters",
    "redshift:DescribeLoggingStatus",
    "s3:GetBucketLocation",
    "s3:GetBucketLogging",
    "s3:GetBucketNotification",
    "s3:GetBucketTagging",
    "s3:ListAllMyBuckets",
    "s3:ListBucket",
    "s3:PutBucketNotification",
    "sqs:GetQueueAttributes",
    "sqs:ListQueues",
    "sqs:ListQueueTags",
    "tag:GetResources",
   ],
   "Resource": "*"
  }
 ]
}
```
  
  
[Back to the Lab Index](../README.md#get-shirt-hot-with-splunk)
  
