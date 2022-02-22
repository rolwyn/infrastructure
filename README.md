# infrastructure

1. AWS create vpc #1
aws cloudformation create-stack --stack-name devvpc --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.1.0.0/24"

2. aws cloudformation create-stack --stack-name devvpc --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=AZone1,ParameterValue="a" ParameterKey=AZone2,ParameterValue="b" ParameterKey=AZone3,ParameterValue="c" --region us-east-1

3. aws cloudformation create-stack --stack-name devvpc-1 --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.2.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.2.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.2.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.2.3.0/24" ParameterKey=AZone1,ParameterValue="a" ParameterKey=AZone2,ParameterValue="b" ParameterKey=AZone3,ParameterValue="c" --region us-east-1

<!-- Delete stack -->
aws cloudformation delete-stack --stack-name devvpc --region us-east-1

<!-- Set profile and region -->
export AWS_PROFILE=dev
export AWS_REGION=us-east-1
