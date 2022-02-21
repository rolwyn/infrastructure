# infrastructure

1. AWS create vpc #1
aws cloudformation create-stack --stack-name devvpc --template-body file://cfvpc.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.1.0.0/24"

2.