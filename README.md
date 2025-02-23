**API Gateway Integration with AWS Lambda**

This project demonstrates how to set up an API Gateway locally using AWS SAM and integrate it with a simple AWS Lambda function. The API Gateway will trigger a Lambda function that returns a "Hello, World!" response.

**Prerequisites**

    - AWS CLI installed and configured

    - AWS SAM CLI installed (Serverless Application Model)

    - Docker installed for running the Lambda function and API Gateway locally

    - Visual Studio Code (optional but recommended)

**Setting Up API Gateway Locally Using AWS SAM**

    1. Initialize a New AWS SAM Application

    Open your terminal in VS Code and run:
    
        sam init

    Choose the following options:

        Template: AWS Quick Start Templates
        
        Runtime: Python 3.9
        
        Project Type: Hello World Example

   
    2. Start an API Gateway Locally

        sam local start-api

    3. Access the API

        curl http://127.0.0.1:3000/hello
        
        Or open your browser and go to: http://127.0.0.1:3000/hello

**Creating a Basic Lambda "Hello World" with API Gateway**

 **  _ hello_world/app.py_**

        def lambda_handler(event, context):
            return {
                "statusCode": 200,
                "body": "Hello, World!"
            }

 ** _  template.yaml_**

    AWSTemplateFormatVersion: '2010-09-09'
    Transform: AWS::Serverless-2016-10-31
    
    Resources:
      HelloWorldFunction:
        Type: AWS::Serverless::Function
        Properties:
          Handler: hello_world.app.lambda_handler
          Runtime: python3.8
          Events:
            Api:
              Type: Api
              Properties:
                Path: /hello
                Method: get
    
**Expected Output**
    
    {
      "statusCode": 200,
      "body": "Hello, World!"
    }


