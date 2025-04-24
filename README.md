Pre-Setup: 
1.	AWS EC2 instance to host Jenkins.
2.	Git installed on local system or EC2.
3.	GitHub account.
4.	Git Bash installed on local Windows machine.

Step-by-Step:

Step 1: Create EC2 Instance (on AWS Console)
•	Launch an EC2 instance (jenkins-ci)
•	Ensure that port 22 (SSH) and port 8080 (Jenkins) are allowed in the Security Group.

Step 2: SSH into EC2
SSH into EC2 instance to install and update
ssh -i "/c/Users/Chithra/Downloads/my.pem" ubuntu@13.232.145.34
sudo apt update && sudo apt upgrade -y

Step 3: Install Git on EC2 
Inside the EC2 terminal, Install Git.
sudo apt update
sudo apt install git -y

Step 4: Install Jenkins on EC2
-----Inside the EC2 terminal install Jenkins.
1.	Install Java 
sudo apt install openjdk-17-jdk -y
2.	Add Jenkins repository and key
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
3.	Update and install Jenkins:
sudo apt update
sudo apt install jenkins -y
Jenkins -v

4.	Start Jenkins:
sudo systemctl start jenkins
sudo systemctl enable Jenkins

-----Install Docker in Jenkins:
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg echo \ "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \ https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
sudo usermod -aG docker Jenkins
sudo systemctl restart jenkins

-----kubernets in Jenkins:
curl -LO "https://dl.k8s.io/release/$(curl -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version --client

Add kubeconfig File (Credentials)

Step 5: Access Jenkins in Browser
•	Open browser and access Jenkins 
•	Get the initial admin password from your EC2 instance terminal:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
•	Use this password to unlock Jenkins in the browser, and complete the setup by installing the suggested plugins.
