# Report
## Repository:
### Infrastructure
- AWS: https://github.com/anhquan99/sd4866_aws_infrastructure
- Azure: 
- GCP:  
### MSA
- https://github.com/anhquan99/sd4866_msa
## AWS
- To setup EC2 to host Jenkins, SonarQube and Trivy you can reference: https://github.com/nashtech-garage/jenkins-devops-ci, build this EC2 to AMI.
- This EC2 is using pre built AMI which enable user to run without to install everytime the infrastructure deployed.
- Setup AWS CLI:
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
- **Note**:
    - When using EC2 to host Jenkins the minimum RAM required to use Jenkins is 8GB.
    - The security group should allow all outbound connection for Jenkins to download plugins.
    - When Jenkins is running slow, check for the Jenkins URL. If the Jenkins URL is not the same as the IP of the EC2 then replace the EC2 IP because Jenkins save the last EC2 IP which was build to AMI.
### Setup Jenkins
- Download plugins:
    - Docker Pipeline
    - SonarQube Scanner for Jenkins
    - Pipeline: AWS Step
    - Kubernetes
- Setup Jenkins with SonarQube: https://www.youtube.com/watch?app=desktop&v=KsTMy0920go
- Config SonarQube in Jekins:
    - Manage Jenkins -> System -> Set configuration ![alt text](/assets/image.png)
    - Manage Jenkins -> System -> Set configuration ![alt text](/assets/image-1.png)
- Setup Jenkins credentials ![alt text](/assets/image-7.png)
- Setup Jenkins Node with label `Built-In' ![alt text](/assets/image-5.png)
- Setup AWS IAM: AWS -> IAM -> Users -> create user -> Security credentials -> create access token ![alt text](/assets/image-4.png)
### Setup multibranch pipeline
- Configuration ![alt text](/assets/image-2.png) ![alt text](/assets/image-3.png)
### Setup SonarQube
- Create webhook for Jenkins ![alt text](/assets/image-6.png)
### Scenario without ArgoCD
- Scan Trivy will be error too many request when you set parallel pipeline because when running trivy it will download the database every run so you should run in 1 pipeline and skip downloading database the second run.
- Result:
![alt text](/assets/image-8.png)
![alt text](/assets/image-10.png)
![alt text](/assets/image-11.png)
![alt text](/assets/image-12.png)
![alt text](/assets/image-13.png)
![alt text](/assets/image-14.png)
![alt text](/assets/image-15.png)