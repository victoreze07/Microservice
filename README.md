1. Install Jenkins for Automation:

##Install Jenkins on the EC2 instance to automate deployment: Install Java

sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version

##jenkins
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins

Access Jenkins in a web browser using the public IP of your EC2 instance.
publicIp:8080


2. Set up Docker on the EC2 instance:

sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER  # Replace with your system's username, e.g., 'ubuntu'
newgrp docker
sudo chmod 777 /var/run/docker.sock


3. Security

Install SonarQube and Trivy:
Install SonarQube and Trivy on the EC2 instance to scan for vulnerabilities.

##sonarqube
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community

To access:
publicIP:9000 (by default username & password is admin)

To install Trivy:

sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy  


##To scan image using trivy
trivy image <imageid>

