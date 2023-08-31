# demo-ngnix-app
Creation of a terraform deployment to host a stateless application in AWS
Prerequisites
Terraform installed in configured in your system
AWS CLI configured 
Docker engine
Steps I used during this are as follows:

I have created a docker file and used this https://hub.docker.com/r/nginxdemos/hello/ and created a basic index.html page

I have build the image and ran the docker container in the local machine and then used http://localhost:8080 to confirm if the container is running properly.

![image](https://github.com/nileshk12/demo-ngnix-app/assets/96992736/c1e154cf-d3dc-415e-a609-79ce7823beeb)

Then I have created an AWS account and created a user Terraform_ECS and downloaded the access credentials.

The next steps I started creating the main.tf file for Terraform, the following resources I created using the terraform scripts

I provided AWS resource provider from hasicorp

Then added my default AWS region and my IAM access keys which I already had downloaded

Then I created a AWS ECR repository in AWS, before contnuing to the next steps I pushed my docker image from local to ECR repo.
![image](https://github.com/nileshk12/demo-ngnix-app/assets/96992736/a1adc3b2-bf95-4280-8b07-2c316d3d1602)

THen I created AWS ECS cluster and ECS task definition and added a parameter for the ECR repo image uri
![image](https://github.com/nileshk12/demo-ngnix-app/assets/96992736/7726d812-9b28-45a4-8edd-f0e5c5cdc471)

![image](https://github.com/nileshk12/demo-ngnix-app/assets/96992736/7848f158-0944-469f-bac7-85711b3ca02d)

Then I had to create a IAM role for ECS to execute the task execution

Next I started adding the VPC ,Subnets and Application Load Balancer in the file

![image](https://github.com/nileshk12/demo-ngnix-app/assets/96992736/23b3b8d2-9c0d-44db-9220-c11b0eb6a257)
![image](https://github.com/nileshk12/demo-ngnix-app/assets/96992736/f37f162d-cd65-47b3-b3af-9d056e0b62fb)


I created SG for the LB for the ports required for the application to run 
![image](https://github.com/nileshk12/demo-ngnix-app/assets/96992736/a92e97aa-f6d8-4b00-a2a8-c7052f864ecb)

Then I created LB listners and target groups

Then I created ECS app service with launch type Fargate and desired count as 3 and added the network configurations by passing subnet details and Security Groups.

The next step I created a security group for the aws services so that traffic is only allowed from the LB security group.

The next step I added the output parameter to get the LB url to open the application
![image](https://github.com/nileshk12/demo-ngnix-app/assets/96992736/56bc7bd7-5bc5-4218-b92d-7b662086e241)

![image](https://github.com/nileshk12/demo-ngnix-app/assets/96992736/7c0c2288-0bc5-4086-b0d0-09ba86c895b9)


After creation of the main.tf file I did run the below commands

terraform validate (to check if all is good in the main.tf file)

terraform plan (to see all the resources that are getting created)

terraform apply (to create all the resources in AWS)

terraform destroy (to stop and remove all the resources)


