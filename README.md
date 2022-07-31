## Cli command to deploy
cd cfn/
cfn-lint *.yaml
aws cloudformation deploy --template-file vpc.yaml --region ap-southeast-2 --stack-name myrha-vpc
aws cloudformation deploy --template-file domain.yaml --region ap-southeast-2 --stack-name myrha-domain
aws cloudformation deploy --template-file ssm-domain-join.yaml --region ap-southeast-2 --stack-name myrha-ssm-domain-join
aws cloudformation deploy --template-file ssm-adgroup-creatandjoin.yaml --region ap-southeast-2 --stack-name myrha-ssm-adgroup-creanteandjoin
aws cloudformation deploy --template-file ssm-credspec-generator.yaml --region ap-southeast-2 --stack-name myrha-ssm-credspec-generator
aws cloudformation deploy --template-file ecs.yaml --region ap-southeast-2 --stack-name myrha-ecs --capabilities CAPABILITY_IAM
aws ssm get-document --name $credspec_ssm_doc | jq -r .Content > creds.json
aws s3 cp creds.json  s3://rha-bucket/
aws cloudformation deploy --template-file iam.yaml --region ap-southeast-2 --stack-name myrha-iam --capabilities CAPABILITY_IAM
aws cloudformation deploy --template-file external-alb.yaml --region ap-southeast-2 --stack-name myrha-alb
```


          dockerSecurityOptions:
            - "credentialspec:file://qadomain_acp.json"      


