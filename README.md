# ToolsCommands

Jenkins - Install Commands
------------------------
yum install java-21-amazon-corretto -y
sudo wget -O /etc/yum.repos.d/jenkins.repo     https://pkg.jenkins.io/rpm-stable/jenkins.repo
yum install jenkins -y
systemctl start jenkins
systemctl status jenkins
systemctl enable jenkins

Sonar Commands
-----------------------
#! /bin/bash
#Launch an instance with 9000 and t2.medium
cd /opt/
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.6.50800.zip
unzip sonarqube-8.9.6.50800.zip
yum install java-17-amazon-corretto -y
useradd sonar
chown sonar:sonar sonarqube-8.9.6.50800 -R
chmod 777 sonarqube-8.9.6.50800 -R
su - sonar

#run this on server manually
#sh /opt/sonarqube-8.9.6.50800/bin/linux/sonar.sh start
#echo "user=admin & password=admin"


Tomcat - install Commands
------------------------
yum install java-21-amazon-corretto -y
wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.121/bin/apache-tomcat-9.0.121.tar.gz
tar -zxvf apache-tomcat-9.0.121.tar.gz
sed -i '56 a\<role rolename="manager-gui"/>' apache-tomcat-9.0.121/conf/tomcat-users.xml
sed -i '57 a\<role rolename="manager-script"/>' apache-tomcat-9.0.121/conf/tomcat-users.xml
sed -i '58 a\<user username="tomcat" password="admin@123" roles="manager-gui, manager-script"/>' apache-tomcat-9.0.121/conf/tomcat-users.xml
sed -i '59 a\</tomcat-users>' apache-tomcat-9.0.121/conf/tomcat-users.xml
sed -i '56d' apache-tomcat-9.0.121/conf/tomcat-users.xml
sed -i '21d' apache-tomcat-9.0.121/webapps/manager/META-INF/context.xml
sed -i '22d' apache-tomcat-9.0.121/webapps/manager/META-INF/context.xml
sh apache-tomcat-9.0.121/bin/startup.sh