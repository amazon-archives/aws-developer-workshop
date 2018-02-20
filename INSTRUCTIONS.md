![](images/1.png)

Table of Contents

* [Overview](#overview)

* [Introduction](#intro)

* [Launching a development toolchain using AWS CodeStar](#devtool)

* [Writing your first AWS Lambda Function on AWS Cloud9](#cloud9)

* [Deploying Your Function using AWS SAM and AWS CodeDeploy](#sam)

* [Debugging and Monitoring your function](#debug)

* [Clean up](#cleanup)

* [Conclusion](#conclusion)


<a name="overview"></a>
# Overview

With services like AWS CodeStar, AWS Cloud9, AWS Lambda and Amazon API Gateway, developers can very easily develop, debug, and deploy serverless applications in the cloud.

AWS CodeStar enables you to quickly develop, build, and deploy applications on AWS. AWS CodeStar provides a unified user interface, enabling you to easily manage your software development activities in one place. With AWS CodeStar, you can set up your entire continuous delivery toolchain in minutes, allowing you to start releasing code faster.

AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. With Cloud9, you can quickly share your development environment with your team, allowing you to pair program and track each other&#39;s inputs in real-time.

AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume - there is no charge when your code is not running. With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code and Lambda takes care of everything required to run and scale your code with high availability.

In this Lab, you will experience:

- Launching development tools for building a serverless application using AWS CodeStar.
- Developing your first AWS Lambda function.
- Deploying your first AWS Lambda function using AWS SAM (Serverless Application Model).
- Testing and debugging your AWS Lambda function in AWS Cloud9 and AWS SAM Local.

**Important:** Many of the steps in this lab involve resolving errors that have been built in to the provided starter files (in step 17). This approach will show how the IDE can be used to develop, test and deploy serverless applications.


<a name="intro"></a>
# Introduction

In this hands-on lab, we are going to start with a Hello World node.js serverless app that returns a static web page. As part of this lab, we will be developing, testing, debugging and deploying a new serverless function for adding 2 numbers. The high level architecture is as follows:

  * TODO_IMAGE_HERE

<a name="devtool"></a>
# Launching a development toolchain using AWS CodeStar

1. Sign into the AWS Management Console [https://console.aws.amazon.com/](https://console.aws.amazon.com/).

**Note:** For this lab you will need to use an IAM user and not a federated user account. The account will require _AWSCodeStarFullAccess_ managed policy. Alternatively, you can create projects if you have an IAM administrative user with full permissions for all AWS Services (_AdministratorAccess_ managed policy). For more information, see [Setting up AWS Code Star (Step 3: Create or Use an IAM User).](https://docs.aws.amazon.com/codestar/latest/userguide/setting-up.html#setting-up-create-iam-user)
2. In the upper-right corner of the AWS Management Console, confirm you are in the desired AWS region (e.g., N. Virginia).
3. Click on **AWS CodeStar** from the list of all services.
4. Click on **Start a project**.
5. If this is the first time you use the service, you will be prompted to create the required service roles for AWS Code \* services. Select **Yes, create role**.

1. Choose a project template:
Under _Application Category_ select _Web Application._
Under _Programming Languages_ select _Node.js._
Pick _Node.JS Web Application AWS Lambda (running serverless)._

 

1. Enter the project details:
Project name: _serverless-lab._
Which repository do you want to use? _AWS CodeCommit._
Click **Next**.

 

1. Leave everything as the default and click on **Create Project**. If this is the first time you use the service, you will also be prompted to enter your display name and email.
2. We are going to use AWS Cloud9 as our IDE. Select AWS Cloud9 and hit **Next.**
3. For our instance, we will select _t2.small_. We will leave the networking settings as default which will launch the instance in our default VPC in a public subnet. Under _Cost-saving_ settings, observe that the environment will be automatically shut down after 30 minutes. Click **Next**.
4. AWS CodeStar is now provisioning all the AWS Code \* services. This process may take around 3-5 minutes.

 

1. While you wait, open up a new browser tab and go to the [IAM Roles console](https://console.aws.amazon.com/iam/home?region=us-east-1#/roles) (listed under Services). Search for _&#39;code&#39;_ and notice that AWS CodeStar created new IAM Roles for each of the AWS service we are going to use.

 

1.
13.Head back to the _AWS CodeStar Dashboard_ and scroll to the _Application endpoints_ panel.

 
2. Click on the endpoint URL. You should see a &quot;Hello World&quot; web page rendered by Node.js. Congratulations! You successfully configured an end-to-end development and continuous deployment pipeline on AWS.

<a name="cloud9"></a>
# Writing your first AWS Lambda Function on AWS Cloud9

1. Go back to the AWS CodeStar dashboard, and click on **IDE** on the left pane.
Click **Open IDE.**

 

| **Note:**
 


 |

You use the AWS Cloud9 IDE, running in a web browser on your local computer, to interact with your environment. An Amazon EC2 instance or your own server connects to the environment. An environment is a place where you store your project&#39;s files and where you run the tools to develop your apps.You use the AWS Cloud9 IDE to work with files in the environment. You can:
- Store these files locally on the instance or server.
- Clone a remote code repository—such as a repo in AWS CodeCommit—into your environment.
- Work with a combination of local and cloned files in the environment.
 |
| --- | --- |

1. Upon first login, AWS Cloud9 automatically clone a starter project &quot;locally&quot; into our development instance. You should see something like this:


```
user:~/environment $ /tmp/git-cloning-runner-xxx-xxx.sh
Cloning into '/home/ec2-user/environment/serverless-lab'...
remote: Counting objects: 16, done.
Unpacking objects: 100% (16/16), done.

Navigate to your cloned repository by typing "cd /home/ec2-user/environment/serverless-lab" to start working with "https://git-codecommit.us-east-1.amazonaws.com/v1/repos/serverless-lab"

To set your display name run "git config --global user.name YOUR_USER_NAME"
To set your display email run "git config --global user.email YOUR_EMAIL_ADDRESS"

user:~/environment $

```

1. We&#39;re going to create a new API microservice in this project. Perform the following command in the terminal window at the bottom (labeled as _bash – &quot;ip-xx-xx-xx-xx&quot;):_

```
cd serverless-lab
wget https://s3-us-west-2.amazonaws.com/apn-bootcamps/serverless-2018/addservice-01.tar.gz
tar xf addservice-01.tar.gz
rm addservice-01.tar.gz
```

**Note:** In some browsers (E.g. Google Chrome), you may be prompted to download Cloud9 Browser Extension to enable copy-paste between this document, and the AWS Cloud9 IDE inside the browser window.

 

The commands above will add the following files to your local AWS Cloud9 environment:

1.
  1. js – our addition-as-a-service lambda function
  2. test/event.numbers.json – the test payload
  3. .gitignore – instruction for git to ignore temp files

To confirm we have all the files in place, perform ls in the terminal window and you should see the following files:

|
- js
- yml
- js
- \nothing
 |
- \public
- md
- yml
- \test
 |
| --- | --- |

1. We will need to update our SAM template (_template.yml_) to register our new function.
Incorporate these \*\ ***requirements\*\*** by modifying the template.yml file:

1. Function name: &quot;AddService&quot;
2. The functionality will be handled by the handler() function in js
3. Runtime: &quot;10&quot;
4. Use the same LambdaTrustRole
5. The event trigger will be coming from our existing &quot;GetEvent&quot; API Gateway
6. We would like to return a JSON response whenever we receive an _ANY_ HTTP request to the API with path /add/{x}/{y}. Therefore, given [http://[api-address]/add/1/2](http://%5Bapi-address%5D/add/1/2),the API should return { … &quot;result&quot;:3 … }.

**Hint:** Use the _GetHelloWorld_ resource definition in the same file (template.yml) to help you apply the necessary changes.  See [Serverless Resources Within AWS SAM](http://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html) for the complete reference, or use the guide below:

```
AddService:
  Type: AWS::Serverless::Function
  Properties:
    Handler: filename.handler-function
    Runtime: nodejs6.10
    Role:
      Fn::ImportValue:
        !Join ['-', [!Ref 'ProjectId', !Ref 'AWS::Region', 'LambdaTrustRole']]
    Events:
      GetEvent:
        Type: Api
        Properties:
          Path: /path/{x}/{y}
          Method: any
```

1. After you are done making those changes. Let&#39;s test our resource definition locally in our Cloud9 environment to make sure we have defined our new AWS Lambda function correctly. In the terminal window, confirm that you are in
/home/ec2-user/environment/serverless-lab/ and perform the following:

```
sam local invoke "AddService" -e test/event.numbers.json
```

Our add.js currently do not implement the functionality we are seeking. We are expecting to see &quot;Error: Not Implemented&quot; exception. This means we have configured our SAM template correctly.

**Note:** The first time you execute a function, SAM LOCAL will fetch the appropriate Docker image for the function as defined in our template.yml. Once that is done, SAM LOCAL will invoke theLambda function we just wrote, showed the response, _Duration_ and the _Max Memory Used_ metric which is useful for tuning our AWS Lambda function configuration.

1. Open up _add.js_ and implement our add function in line 12-16.

 

1. You think you got it right? Let&#39;s test out the Lambda function locally again:

```
sam local invoke "AddService" -e test/event.numbers.json
```

should return the following:

```
{
    "statusCode":200,
    "body":"{\"result\":116}",
    "headers":{"Content-Type":"application/json, … }
}
```

1. Congratulations! You have implemented add()as an AWS Lambda function.

<a name="sam"></a>
# Deploying Your Function using AWS SAM and AWS CodeDeploy

1. We will now configure our git user in the AWS Cloud9 environment so we can commit our changes to the code repository

```
git config --global user.email you@example.com
git config --global user.name "Your Name"
```

2. We are going to add all our pending changes, commit it to Git and push it to our AWS CodeCommit Repository:

```
git add -A
git commit -m "add add-as-a-service"
git push origin master

```


1. By default, AWS CodeStar configured AWS CodeBuild to deploy on every code commits. Go back to your AWS CodeStar serverless-lab dashboard. You can see the status of the current build, or see more details about the build by selecting **Build** from the left hand pane. You will notice that a build is currently taking place. This will take around 2 minutes.

 

**Note:** You can also deploy the AWS Lambda function manually, by executing the following commands. You will need to provide S3 bucket location, CloudFormation Stack name and other parameters that the CloudFormation requires.

To create the package on an S3 Bucket:

```
aws cloudformation package \
    --template-file ./template.yml \
    --s3-bucket $S3_BUCKET \
    --s3-prefix $S3_BUCKET_PREFIX_NAME \
    --output-template-file ./template.output.yml \
    --force-upload 
```



To execute the deployment:

```
aws cloudformation deploy \
    --template-file ./template.output.yml \
    --stack-name $STACK_NAME \ # E.g. serverless-lab
    --capabilities CAPABILITY_IAM
    --parameter-overrides ProjectId=$PROJECT_ID # E.g. serverless-lab
```


<a name="debugging"></a>
# Debugging and Monitoring your function

1. After a successful deployment, open the AWS CodeStar project dashboard and copy our _Application endpoints_ location.

 

1.
27.Open up a browser and modify the URL to look something like this:
 [https://xxxx.execute-api.us-east-1.amazonaws.com/Prod/add/2/3](https://xxxx.execute-api.us-east-1.amazonaws.com/Prod/add/2/3)
 
Oh no! It looks like we have a bug. On step 19, we tested the Lambda function add.js in isolation and it performed correctly. However we have not tested the function integrated with the Amazon API Gateway. Head back to our AWS Cloud9 IDE so we can debug this issue.
2. Open add.js and add a breakpoint on line 17 by clicking on the space next to the row number until it is showing a red dot. Click **Run** to start our debugging session.

 

1. Since the bug only appears when the function is called by Amazon API Gateway, we will debug our function using a local API Gateway environment. Enter the following configuration:
  1. Click on the Debug icon
  2. Run on: _API Gateway (local)_
  3. Function: _AddService_
  4. Path: _/add/1/2_
  5. Method: _GET_
  6. Click **Run**

 

1. We should now see the debugger stops at line 17. Observing it closely, we need to make adjustment to line 17 to read from the correct event object properties. Make those changes.

**Hint:** Watch out for the [data types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number#Examples).

1. Let&#39;s test it again using the command line this time:

```
sam local start-api&
```

Press enter.

```
curl http://127.0.0.1:3000/add/25/75
```

We should now receive the right result { … &quot;result&quot;:100 … }

31. Commit our latest changes to AWS CodeCommit again.
```
git add -A
git commit -m "Bugfix: Add() now performs correctly on API GW"
git push origin master
```
32.	Wait for our Continuous Deployment pipeline to complete, and test it from our live endpoint that looks similar to: https://xxxx.execute-api.us-east-1.amazonaws.com/Prod/add/25/75  

33. Congratulations, you have completed the lab.

<a name="cleanup"></a>
# Clean up

After you are done with your lab, head over to the CloudFormation console (listed under Services) and delete aws-cloud9-serverless-lab-xxxxxx, awscodestar-serverless-lab-lambda, and awscodestar-server-lab stacks. This will delete all the resources we created during this lab.

<a name="conclusion"></a>
# Conclusion

In this lab you have learned creating end-to-end development tools using AWS CloudStar, writing your first Serverless microservice using AWS Lambda and Amazon API Gateway using the AWS Cloud9 IDE.
