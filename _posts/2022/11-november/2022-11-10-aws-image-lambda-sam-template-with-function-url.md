---
title: "AWS Image Lambda SAM template with function URL"
categories: ["aws", "lambda", "sam"]
---


`template.yml` file:
```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Description: hello-app
Parameters:
  environment:
    Type: String
    Default: development
    Description: Enter the name of cluster for deploy.

Resources:
  HelloFunction:
    Type: AWS::Serverless::Function # More info about Function Resource: https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessfunction
    Properties:
      FunctionName: !Sub hello-app-${environment}
      PackageType: Image
      MemorySize: 3000
      Timeout: 600
      Architectures:
        - x86_64
      FunctionUrlConfig:
        AuthType: NONE
        Cors:
          AllowOrigins:
            - '*'
    Metadata:
      DockerTag: hello-v1
      DockerContext: ./
      Dockerfile: Dockerfile

Outputs:
  HelloFunctionUrlEndpoint:
    Description: "My Lambda Function URL Endpoint"
    Value: !GetAtt HelloFunctionUrl.FunctionUrl
```

`publish.sh` file:
```bash
#!/bin/bash

sam build
sam deploy --stack-name=ngc-app-stack-development --region=eu-west-1
```

`Dockerfile` file:
```dockerfile
FROM public.ecr.aws/lambda/nodejs:10
COPY / ${LAMBDA_TASK_ROOT}
RUN npm install --save
CMD [ "app.handler" ]
```