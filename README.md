

#Open Source Project: DevSecOps for OpenAI Chatbot UI Deployment | DevSecOps

The open-source AI chat app for everyone.
![image](https://github.com/user-attachments/assets/2e073d94-0e49-4e43-a8b0-72fb4ee3f22b)

![image](https://github.com/user-attachments/assets/6a81adf7-2743-4016-a1bc-bf92ce3a46b1)
In today’s digital landscape, user engagement is key to the success of any application. From websites to mobile apps, providing users with interactive and personalized experiences is essential. That’s why we’re thrilled to announce our latest endeavor:

What is ChatBOT?

ChatBOT is an AI language model trained on vast amounts of human conversation data. It’s capable of generating human-like text responses based on the input it receives. From answering questions to engaging in conversation, ChatBOT can simulate natural language interactions with users, making it an invaluable tool for enhancing user engagement.

Why ChatBOT?

Personalized Interactions: ChatBOT can understand and respond to user queries in a natural and conversational manner, creating personalized interactions that keep users engaged.
24/7 Availability: Unlike human agents, ChatBOT is available 24/7 to assist users, providing instant responses to their queries and ensuring a seamless user experience.
Scalability: With ChatBOT deployed in our application, we can handle a large volume of user interactions without compromising performance, ensuring scalability as our user base grows.
How We’re Deploying ChatBOT

To deploy ChatBOT on our EKS, we’re leveraging Jenkins as our CICD (Continuous Integration/Continuous Deployment) tool and deploying the chatbot within a Docker container. This approach allows us to automate the deployment process, ensuring efficient and reliable delivery of updates and enhancements to our users
now here are the few steps to deploy open AI using devsecops
Launch an Ubuntu(22.04) T2 Large Instance
Create IAM role
Install Jenkins, Docker and Trivy
#!/bin/bash
sudo apt update -y
wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | tee /etc/apt/keyrings/adoptium.asc
echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | tee /etc/apt/sources.list.d/adoptium.list
sudo apt update -y
sudo apt install temurin-17-jdk -y
/usr/bin/java --version
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
                  /usr/share/keyrings/jenkins-keyring.asc &gt; /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
                  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
                              /etc/apt/sources.list.d/jenkins.list &gt; /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl start jenkins

sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER   #my case is ubuntu
newgrp docker
sudo chmod 777 /var/run/docker.sock

docker run -d --name sonar -p 9000:9000 sonarqube:lts-community

#Install Trivy, Kubectl,Terraform
sudo apt-get install wget apt-transport-https gnupg lsb-release -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg &gt; /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy -y
# Install Terraform
sudo apt install wget -y
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update &amp;&amp; sudo apt install terraform
# Install kubectl
sudo apt update
sudo apt install curl -y
curl -LO https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
# Install AWS CLI
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt-get install unzip -y
unzip awscliv2.zip
sudo ./aws/install

Install Plugins like JDK, Sonarqube Scanner, NodeJs, OWASP Dependency Check
Install Plugin
Goto Manage Jenkins →Plugins → Available Plugins →

Install below plugins

Blue ocean

1 → Eclipse Temurin Installer

2 → SonarQube Scanner

3 → NodeJs Plugin

4 → Docker

5 → Docker commons

6 → Docker pipeline

7 → Docker API

8 → Docker Build step

9 → Owasp Dependency Check

10 → Kubernetes

11 → Kubernetes CLI

12 → Kubernetes Client API

13 → Kubernetes Pipeline DevOps steps

using jenkins configure the tools, system files, credenditals

run the pipeline script

copy the public ip:3000
 













