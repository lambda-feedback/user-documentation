# Deployment notes
---
**Warning** Very messy notes ahead

---

- https://npm.runkit.com/mathml-to-latex

- CodeCommit -> CodeBuild -> AWS ECR -> ECS or Fargate (load balancers)
- Elastic Beanstalk for DB Wrapper 
- Paper on converting from Mongo to DynamoDB
- CloudFront distribution + caching to save money
	- [https://aws.amazon.com/cloudfront/getting-started/S3/](https://aws.amazon.com/cloudfront/getting-started/S3/ "https://aws.amazon.com/cloudfront/getting-started/s3/")

- Setup AWS Organisation
	- If not enough time to migrate everything else over:
	- Setup VPN Peering so that virtual cloud can talk to each other 
	- Update routing tables  so that VPC can talk to each other
	- Security groups 
- SDK Cloudformation, Infrastructure as code

- Create root account 
- Setup MFA sign -in 
- Create a new IAM user give all admin perms 
- Keep Security keys and passwords

- [DB Stuff](https://aws.amazon.com/pm/documentdb/?trk=ps_a134p000007CAOwAAO&trkCampaign=acq_paid_search&sc_channel=PS&sc_campaign=acquisition_GB&sc_publisher=Google&sc_category=Database&sc_country=GB&sc_geo=EMEA&sc_outcome=acq&sc_detail=%2Bmongodb&sc_content=MongoDB_bmm&sc_matchtype=b&sc_segment=536240534618&sc_medium=PAC-PaaS-P|PS-GO|Non-Brand|All|PA|Database|DocumentDB|GB|EN|Text|xx|SEM|PMO21-05620&s_kwcid=AL!4422!3!536240534618!b!!g!!%2Bmongodb&ef_id=CjwKCAjwhaaKBhBcEiwA8acsHNbokEcDhpMjCqFc3gpSqhErVN7hiIsVtD5XNmVDibdmyFpUp9o8_RoC47gQAvD_BwE:G:s&s_kwcid=AL!4422!3!536240534618!b!!g!!%2Bmongodb)

- [DB migration](https://aws.amazon.com/blogs/database/performing-a-live-migration-from-a-mongodb-cluster-to-amazon-dynamodb/)

- [DB More stuff](https://aws.amazon.com/blogs/apn/connecting-applications-securely-to-a-mongodb-atlas-data-plane-with-aws-privatelink/ "https://aws.amazon.com/blogs/apn/connecting-applications-securely-to-a-mongodb-atlas-data-plane-with-aws-privatelink/")
	- Privatelink is pricey




- Infrastructure as code: terraform or polami
	- No serverless framework
	- `Serverless next.js`
	- [https://github.com/serverless-nextjs](https://github.com/serverless-nextjs)
- Access token on admin website 
- TypeScript for React
- GraphQL on api?
- GRPC, Protobuf
- DynamoDB, ElastiCache for quick db on Grading Gateway
- EC2, ECS or Kubernetes architecture for grading gateway when users start rolling in
- Amplify dont use, use EB
	- Next.js
	- Cloudfront Distribution
	- AWS S3 Sync  location of bundle  S3 Bucket 
- CSS-in-JS instead of CSS modules



- **Express on Lambda, library on github**!!!
	- `Express.js` has too much control 
	- `Nest.js` instead? 
	- `ApolloServe` - GraphQL


- Grading gateway:
	- Define initialisation client outside of the lambda function handler 
- CloudWatch Event to keep alive to stop the cold start
- No need to DynamoDB right now:
	- Not very consistent
	- Crafting the table depends on the way we query it 
		- (range and partition)
- Could switch to a SQL database 
- `SupaBase` Relational database as a service.

- Setup `Sentry` -> docker image digest -> what build caused issues
	- Really get info about how errors occured 

- SnowPlough pipeline
	- Injests data 
	- Elastic Search for data analytics 
	- 

- Get through iframe isolation using APIs


