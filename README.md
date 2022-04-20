# IAC using AWS CloudFormation

```Name: Rolwyn Quadras, NUID - 001554737, Email - quadras.r@northeastern.edu```

The following steps creates a stack on the AWS using a cloudformation template (csye6225-infra)

# Stack Creation

<!-- Stack creation -->
1. aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=AmiId,ParameterValue="ami-04b58d95458802d3e" --region us-east-1 --profile=dev

<!-- Another stack with different cidr for vpc, subnets -->
2. aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.2.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.2.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.2.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.2.3.0/24" ParameterKey=AZone1,ParameterValue="a" ParameterKey=AZone2,ParameterValue="b" ParameterKey=AZone3,ParameterValue="c" --region us-east-1 --profile=dev

<!-- Stack for private subnets and rdb-->
3. aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=PrivateSubCidrBlock1,ParameterValue="10.1.4.0/24" ParameterKey=PrivateSubCidrBlock2,ParameterValue="10.1.5.0/24" ParameterKey=PrivateSubCidrBlock3,ParameterValue="10.1.6.0/24" ParameterKey=AmiId,ParameterValue="ami-04b58d95458802d3e" --region us-east-1 --profile=dev  --capabilities CAPABILITY_NAMED_IAM

<!-- Delete stack -->
# Delete Stack
aws cloudformation delete-stack --stack-name appstack --profile=demo --region us-east-1

<!-- Set profile and region -->
# Set Profile
export AWS_PROFILE=demo
export AWS_REGION=us-east-1 
# Stack with rds and s3
aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=PrivateSubCidrBlock1,ParameterValue="10.1.4.0/24" ParameterKey=PrivateSubCidrBlock2,ParameterValue="10.1.5.0/24" ParameterKey=PrivateSubCidrBlock3,ParameterValue="10.1.6.0/24" ParameterKey=S3BucketName,ParameterValue="asdafglorious.dev.rolwynquadras.me" ParameterKey=AmiId,ParameterValue="ami-04b58d95458802d3e" --region us-east-1 --profile=dev  --capabilities CAPABILITY_NAMED_IAM

S3 bucket commands
aws s3 rm s3://bucketname --recursive --profile=dev
aws s3api delete-bucket --bucket bucketname --region us-east-1 --profile=dev

# AutoScaling
aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=PrivateSubCidrBlock1,ParameterValue="10.1.4.0/24" ParameterKey=PrivateSubCidrBlock2,ParameterValue="10.1.5.0/24" ParameterKey=PrivateSubCidrBlock3,ParameterValue="10.1.6.0/24" ParameterKey=S3BucketName,ParameterValue="asdafglorious.demo.rolwynquadras.me" ParameterKey=AmiId,ParameterValue="ami-033b95fb8079dc481" ParameterKey=sshKeyName,ParameterValue="awsdemo" ParameterKey=currentEnv,ParameterValue="prod" ParameterKey=SSLCertificateArn,ParameterValue="arn:aws:acm:us-east-1:605680160689:certificate/6fc01231-68ec-4ff9-adda-a780256cc653" --region us-east-1 --profile=demo  --capabilities CAPABILITY_NAMED_IAM

# CodeDeploy Stack
aws cloudformation create-stack --stack-name codedeploystack --template-body file://ci-cd-infra.yml --parameters ParameterKey=CodeDeployBucketName,ParameterValue="codedeploy.rolwynquadras.me" --region us-east-1 --profile=demo --capabilities CAPABILITY_NAMED_IAM

# Cloudwatch logs added

# Adding SSL Certificate to Amazon Certificate Manager
aws acm import-certificate --certificate fileb://prod_rolwynquadras_me.crt --certificate-chain fileb://prod_rolwynquadras_me.ca-bundle --private-key fileb://mypvkey.pem --profile=demo