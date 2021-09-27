# Lambda

TODOS

- cold start and warm start
- can be combine with mutple service: API Gateway, SNS, SQS, Step Function to build serverless
- Concurrey: 1000 (can be increaed by loggin ticket)
-  Support many runtime: nodejs, ruby, python
-  Cost by execution time + requested resource (ram)
-  To intergatre with API gateway, must be return 
statusCody:
body
- Hanler example
```
const handler = (event, context, callback)
```

- Defaul timeout 30min
- To integrate with authrozation and authentication, you can use Cognito or use Lambda CUstom Authorizer
- tmp: 512mb and it 's emepheral
- Tracing: X-Ray
- Logging:: enable CreateLog in CloudWatch into role. Each Lambda function has a role to defined what resource Lamda can access
- Layer: to custom your binary file, for e.g you want to use ffmpeg so you can upload your layer and use it

- Best practice: 
+ If you function need to connnect database, put your connection outside of handler
+ Do not allocate Lamda into VPC, if you donot fully understand it


- Libray
 + middy