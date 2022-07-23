# ecs-ec2
Infrastructure to build ECS on EC2 (not fargate)

# Installation
```
cd cfn/

aws cloudformation deploy --template-file vpc.yaml --stack-name my-rha-vpc
aws cloudformation deploy --template-file ecs.yaml --stack-name my-rha-ecs --capabilities CAPABILITY_IAM 
aws cloudformation deploy --template-file alb.yaml --stack-name my-rha-alb
aws cloudformation deploy --template-file service.yaml --stack-name my-rha-service --capabilities CAPABILITY_IAM
```
