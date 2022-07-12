# AWS

## Java SDK
* [v1](https://github.com/aws/aws-sdk-java)
* [v2](https://github.com/aws/aws-sdk-java-v2/#using-the-sdk)
* [How will you migrate from sdk v1 to v2](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/migration.html)



## AWS Lambda
* [What?](https://youtu.be/AK6Rf_yjvI0?t=11024)
  * AWS Lambda is a serverless computing service provided by Amazon to reduce configuration of server OS.
  * It lets you run code without provisioning or managing servers-it scales automatically and only charges for the time your code is running.
* [When to use](https://youtu.be/AK6Rf_yjvI0?t=11060)
  * When you want to expose an endpoint, a stream processor, or a task to cloud without depending on the server.

* [Advantages:](https://youtu.be/AK6Rf_yjvI0)
  * No need to pay for idle capacity. Pay as you go model.
  * Flexible scaling
  * Zero server management




## SQS
* [How will you implement Producer/Consumer using  **AWS SQS** & Publisher/Subscriber using **AWS SNS** with **Spring Boot** ](https://cloud.spring.io/spring-cloud-static/spring-cloud-aws/2.0.0.RELEASE/multi/multi__messaging.html)

## SNS
* Amazon Simple Notification Service (Amazon SNS) is a managed service that provides message delivery from publishers to subscribers (also known as producers and consumers). Publishers communicate asynchronously with subscribers by sending messages to a topic, which is a logical access point and communication channel. Clients can subscribe to the SNS topic and receive published messages using a supported endpoint type, such as Amazon Kinesis Data Firehose, Amazon SQS, AWS Lambda, HTTP, email, mobile push notifications, and mobile text messages (SMS).

* [How will you **send and receive messages to and from AWS SQS**](https://youtu.be/AK6Rf_yjvI0?t=8638)
* [How will you **subscribe and publish** message to **AWS SNS**](https://youtu.be/AK6Rf_yjvI0?t=10069)




## S3
* Buckets are region specific, folders are represented as prefix to the object name, max object size is 5TB, to upload more than 5GB, use multipart upload.
* [How will do **versioning** in s3](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/23743652#questions/5886124)
* [What is **SSE-S3, SSE-KMS, SSE-C, Client Side Encrption**](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851534#questions/12532098)
* [How will you **enable encryption for infividual objects** in a bucket and how is it differnent from **enabling encryption at bucket level**](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/23743656#questions/12532098)
* [How will you stop uploading nonencrypted objects to s3 using **bucket policies**, block public access, ACLs](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19729152#questions)
* [How will you create **S3 static website**, enable public access, configure allow putObject access policy](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851546#questions)
* [What is **CORS** in S3](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851548#questions) [How will you **configure CORS**](https://aws.amazon.com/premiumsupport/knowledge-center/s3-configure-cors/)
* [How will you **host a static website** in AWS](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19729172#questions/12532098)
* [What is the Consistency Mode for S3](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851524#questions/12532098)
* [S3 Interview Questions](https://www.techgeeknext.com/aws/aws-s3-interview-questions)


## Elastic BeanStalk
* [Deploy Spring Boot Application with Elastic Beanstalk](https://youtu.be/MBpcmoifpNY?list=PLVz2XdJiJQxxurKT1Dqz6rmiMuZNdClqv&t=523)


### **DynamoDB**, 627


* [How will you implement control **fine grained access** to Dynamo DB](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19730794#questions)
* [How will you do **copy tables** in DynanoDB](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19730794#questions)
* [What will be your strategy to **store objects larger than 400KB** will help of DynamoDB and S3](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19730794#questions)
* [What is the difference between **Concurrent Write**, **Atomic Write**, **Conditional Write**, **Batch Writes**](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/bp-partition-key-sharding.html)
* [How do you perform **write sharding** in Dynamo DB.](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19730778#questions) [Read More...](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/bp-partition-key-sharding.html)
* [What is the will you create a serverless **Session State Cache**](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/19730768#questions)
* [How will you implement **TTL** for item present in Dynamo DB](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/15300310#questions)
* [What are some use cases for DynamoDB Streams](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851530#questions)
* [What is **Dynamo DB Accelarator** DAX, and how is it different from Elasticache](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851418#questions)
* [How does **Optimistic Locking** work in **DynamoDB**](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/12203064#questions)
* [When will you use **GSI** instead of **LSI**](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851416#questions)
* [What is the difference between **Eventually Consistent Read & Strongly Consistent Read**](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/28646574#questions)
* [What do you mean by **Transactional Read/Writes in DynamoDB** and how much RCU & WCU do they consume](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/15300318#questions)

* [What is the difference between **Partition Key** & **Sort Key**](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851406#questions)
* [When can you have **non-unique Partition Key** for a DynamoDB table](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851408#questions)
* [How are **RCU** and **WCU** spread across **Partitions**, When will you choose to use **Standard Capacity Mode** over **Provisioned Capacity mode**](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/11851410#questions)
* [Create a **CRUD Application with DynamoDB**. Used Classes & Annotations DynamoDBMapper @DynamoDBDocument @DynamoDBAttribute @DynamoDBTable(tableName = "Person" @DynamoDBHashKey(attributeName = "personId")
    @DynamoDBAutoGeneratedKey)](https://youtu.be/E0-P978Yqdw?list=PLVz2XdJiJQxxurKT1Dqz6rmiMuZNdClqv)
* [DynamoDB annotations](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBMapper.Annotations.html)

* [How will you query DynamoDB from CLI](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/15300314#questions)

        #!/bin/bash

        # Demo Projection Expression
        aws dynamodb scan --table-name Posts --projection-expression "user_id, content" --region  us-east-1

        # Demo Filter Expression
        aws dynamodb scan --table-name Posts --filter-expression "user_id=:u" --expression-attribute-values '{ \":u\" : { \"S\" : \"alice420\" } } ' --region us-east-1

        # Single API call is made, no matter how many items
        aws dynamodb scan --table-name Posts --region us-east-1

        # Since page size is 1, number of api calls will be equal to the number of items in the table 
        aws dynamodb scan --table-name Posts --region us-east-1 --page-size 1

        # Max Items return an item but also returns a next token
        aws dynamodb scan --table-name Posts --region us-east-1 --max-items 1

        aws dynamodb scan --table-name Posts --region us-east-1 --max-items 1 --starting-token eyJFeGNsdXNpdmVTdGFydEtleSI6IG51bGwsICJib3RvX3RydW5jYXRlX2Ftb3VudCI6IDF9
        
        aws dynamodb scan --table-name Posts --region us-east-1 --max-items 1 --starting-token eyJFeGNsdXNpdmVTdGFydEtleSI6IG51bGwsICJib3RvX3RydW5jYXRlX2Ftb3VudCI6IDJ9