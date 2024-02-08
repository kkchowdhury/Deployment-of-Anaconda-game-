
Deployment of the "ANACONDA IN THE CITY" game :-

1) Created 2 roles in IAM. For the 1st role , the Trusted entity type :- AWS Service , the Use case :- EC2 , permission policy :- AmazonEC2RoleforAWSCodeDeploy, Name :- EC2CodeDeploy. For the 2nd role  , the Trusted entity type :- AWS Service , the Use case :- CodeDeploy , permission policy :- AWSCodeDeployRole, Name :- CodeDeployRole.

2)Create an EC2 instance.Name :- ANACONDA_CICD , Amazon Linux, ANACONDAKEYPAIR, Select existing security group --> Default, IAM instance profile --> EC2CodeDeploy. 
User Data (for Dependencies installations for AMAZON Linux 2):-
#!/bin/bash
sudo yum -y updates
sudo yum -y install ruby
sudo yum -y install wget
cd /home/ec2-user
wget https://aws-codedeploy-ap-south-1.s3.ap-south-1.amazonaws.com/latest/install
sudo chmod +x ./install
sudo ./install auto
sudo yum install -y python-pip
sudo pip install awscli

3)Create Application (CodeDeploy --> Applications). Name :- ANACONDA_CICD. Platform :- EC2/On-premises.

4)Create Deployment group. Name :- ANACONDA_CICD_DP , Service :- CodeDeployRole . Amazon EC2 instances , CodeDeployDefault.AllAtOnce , No Load Balancing needed , Key-Value : Name , ANACONDA_CICD.

5) Create Pipeline. Name :- ANACONDA_CICD_Pipeline . Source--> Github (Version 2) . Then we have to connect to our desired Github repository (i.e, https://github.com/kkchowdhury/ANACONDA-IN-THE-CITY , appspec.yml is the most important file ) by establishing a connection (naming the connection as ANACONDA_CICD_GIT). 

6) I skipped the Build stage. In Deploy stage, I chose AWS CodeDeploy, Application name :- ANACONDA_CICD, Deployment group :- ANACONDA_CICD_DP.

7) In my AWS EC2 instance , I will edit inbound rules and include http for port 80 from anywhere(0.0.0.0/0).We can do the same for ssh also.

8) now we can open the Public IPv4 address of our instance.(replace https by http on the link) and pl,ay the game.


  
