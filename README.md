# check_cloudwatch_rds

## Dependencies

1. **awscli** - http://aws.amazon.com/cli/

	*pip install awscli*

2. **jq** - http://stedolan.github.io/jq/
    
	*yum install jq*

You will need to use `aws configure` to setup IAM credentials according to the documentation [here](http://docs.aws.amazon.com/cli/latest/reference/configure/index.html). The IAM user you supply it should just need read only access to RDS and Cloudwatch.


## Nagios Arguments
-p <aws_profile_name>= AWS configure profile

-n <aws_namespace> = [AWS Namespace](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/aws-namespaces.html) - Don't include `AWS/` on the front since it's in the script

-m <cloudwatch_metric> = [Cloudwatch Metric](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/CW_Support_For_AWS.html)

-t <time_period> = (minutes) Time period to monitor. There are calculations to create a date range, which is required for cloudwatch.

-s <metric_statistic> = Examples: Sum, Average, Maximum, Minimum

-i <instance_identifier> = Example: RDS DB Instance shortname (dev-postgres-01)

-w <nagios_warning_metric> = Different metrics have different measurement units. Look at the `case $METRIC_NAME` section. Examples: ReadIOPS is just a count. FreeStorageSpace and FreeableMemory are in MB.

-c <nagios_critical_metric> = Different metrics have different measurement units. Look at the `case $METRIC_NAME` section. Examples: ReadIOPS is just a count. FreeStorageSpace and FreeableMemory are in MB.

## Nagios Config & Example
Setup your command check.
	
	$USER1$/check_cloudwatch_rds -p $ARG1$ -n $ARG2$ -i $ARG3$ -m $ARG4$ -s $ARG5$ -t $ARG6$ -w $ARG7$ -c $ARG8$

	!production!RDS!dev-postgres-01!FreeStorageSpace!Average!15!70!90!

## About
In its current status this only supports RDS, as that's all I have needs for it with Cloudwatch. I believe it has the basic structure to support other AWS Namespaces and Metrics...I just haven't expanded them to other services I don't use.

## Why

I was tired of never finding a good cloudwatch script that actually used aws-cli, so I wrote my own. I would love to extend it with capabilities to monitor more than just RDS.