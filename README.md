# Create Freestyle job in Jenkins | How to create build job in Jenkins to automate Java build and deployment of WAR into Tomcat 


# prem-requisites:
    • Java Project is setup in GitHub or your SCM
    • Jenkins is up and running

# Change Host Name to Jenkins
sudo hostnamectl set-hostname Jenkins
 sudo apt update
 sudo apt install default-jdk -y
 sudo apt install maven -y
    
   # Jenkins Setup
   # Add Repository key to the system
 curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
 /usr/share/keyrings/jenkins-keyring.asc > /dev/null

# Append debian package repo address to the system

 echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
 https://pkg.jenkins.io/debian binary/ | sudo tee \
 /etc/apt/sources.list.d/jenkins.list > /dev/null

# Update Ubuntu package

 sudo apt install jenkins -y

# Access Jenkins in web browser

      
   # Tomcat is up and running 
   # Change Host Name to Tomcat
sudo hostnamectl set-hostname Tomcat
 sudo apt update
 sudo apt-get install tomcat9 tomcat9-docs tomcat9-admin -y
 sudo cp -r /usr/share/tomcat9-admin/* /var/lib/tomcat9/webapps/ -v
 sudo vi /var/lib/tomcat9/conf/tomcat-
   # add
        <role rolename="manager-script"/>
        <user username="tomcat" password="password" roles="manager-script"/>

 sudo systemctl restart tomcat9

    • Make sure you configure maven installation under Jenkins-->manage Jenkins-> Global Tool Configuration. under maven installation. enter Maven3 as name, enter path of maven installation --> /usr/share/maven and uncheck install automatically option.
    • Also install deploy to container,  Jacoco plugins under Jenkins --> Manage Jenkins --> Manage plug-ins
   # Jacoco plugins 

# Click on Available, type Deploy to container, select it. enter Jacoco, select it. Click on Install without restart.

# Click on without restart.

# steps to automate MyWebApp project in Jenkins:

# 1. Login to Jenkins. Click on New item.

# 2. Enter an item name --> select Free style project.

enter name as myFirstAutomateJob. click OK.

# 3. under source code mgmt, click git. enter Bitbucket URL or GitHub URL
Click on your repo, Copy the url from the browser. Paste the url as Repository URL below.

# Copy this project url

 https://github.com/tahers755/devops-project-sample-java-app.git


Enter main as branch specifier or which ever branch you want to check out.

# 4. select that from drop down.
# 5. under build trigger click on poll scm, enter this value to check

# for every 2 mins --> H/02 * * * *

# 6. Build --> Add build step --> invoke top level maven targets →
# select Maven3 from drop down and goal as clean install

# 7. Click on advanced, enter the path of POM file as --> MyWebApp/pom.xml

# 8. click on Add post build action, select Record Jacoco Code coverage report

# 9. click on Add post build action, select deploy war/ear to container

# for WAR/EAR files enter as 

**/*.war
  # 10. click on Add container , select Tomcat 9.x

 # 11. click on add credentials, enter tomcat as user name and password as password.
 select it from drop down.
 
 # after all jobs configuration buid the job and check 

# 12. tomcat url should be --> http://your_public_dns_name:8080
