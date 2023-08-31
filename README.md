# demo-ngnix-app
Creation of a terraform deployment to host a stateless application in AWS
Prerequisites
Terraform installed in configured in your system
AWS CLI configured 
Docker engine
Steps I used during this are as follows:

I have created a docker file and used this https://hub.docker.com/r/nginxdemos/hello/ and created a basic index.html page
I have build the image and ran the docker container in the local machine and then used http://localhost:8080 to confirm if the container is running properly.

Then I have created an AWS account and created a user Terraform_ECS and downloaded the access credentials.

The next steps I started creating the main.tf file for Terraform, the following resources I created using the terraform scripts
-- I provided AWS resource provider from hasicorp
-- Then added my default AWS region and my IAM access keys which I already had downloaded
-- Then I created a AWS ECR repository in AWS, before contnuing to the next steps I pushed my docker image from local to ECR repo.
-- THen I created AWS ECS cluster and ECS task definition and added a parameter for the ECR repo image uri
-- Then I had to create a IAM role for ECS to execute the task execution
-- Next I started adding the VPC ,Subnets and Application Load Balancer in the file
-- I created SG for the LB for the ports required for the application to run 
-- Then I created LB listners and target groups
-- Then I created ECS app service with launch type Fargate and desired count as 3 and added the network configurations by passing subnet details and Security Groups.
-- The next step I created a security group for the aws services so that traffic is only allowed from the LB security group.
-- The next step I added the output parameter to get the LB url to open the application

After creation of the main.tf file I did run the below commands

terraform validate (to check if all is good in the main.tf file)
terraform plan (to see all the resources that are getting created)
terraform apply (to create all the resources in AWS)
terraform destroy (to stop and remove all the resources)


