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
  
  
##### 1. Terraform
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
  
  
##### 2. Trumpet
  
  
  
##### 3. Splunk Observability
  
  
[Back to the Lab Index](../README.md#get-shirt-hot-with-splunk)
  
