# IAC using AWS CloudFormation

```Name: Rolwyn Quadras, NUID - 001554737, Email - quadras.r@northeastern.edu```

The following steps creates a stack on the AWS using a cloudformation template (csye6225-infra)

# Stack Creation

<!-- Stack creation -->
1. aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=AZone1,ParameterValue="a" ParameterKey=AZone2,ParameterValue="b" ParameterKey=AZone3,ParameterValue="c" --region us-east-1 --profile=demo

<!-- Another stack with different cidr for vpc, subnets -->
2. aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.2.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.2.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.2.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.2.3.0/24" ParameterKey=AZone1,ParameterValue="a" ParameterKey=AZone2,ParameterValue="b" ParameterKey=AZone3,ParameterValue="c" --region us-east-1 --profile=demo

<!-- Delete stack -->
# Delete Stack
aws cloudformation delete-stack --stack-name appstack --profile=demo --region us-east-1

<!-- Set profile and region -->
# Set Profile
export AWS_PROFILE=demo
export AWS_REGION=us-east-1
