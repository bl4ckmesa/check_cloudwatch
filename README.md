# check_cloudwatch_rds

## Dependencies

1. **awscli** - http://aws.amazon.com/cli/

	*pip install awscli*

2. **jq** - http://stedolan.github.io/jq/
    
	*yum install jq*

You will need to use `aws configure` to setup IAM credentials according to the documentation [here](http://docs.aws.amazon.com/cli/latest/reference/configure/index.html). The IAM user you supply it should just need read only access to RDS and Cloudwatch.