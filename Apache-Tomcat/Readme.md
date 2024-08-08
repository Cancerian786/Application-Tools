![DevOpsGuru Banner](https://github.com/Cancerian786/Favicon/blob/main/tomcat.png)

# 🎉 Welcome to DevOpsGuru

🌐 Apache Tomcat Overview

Apache Tomcat is an open-source, Java-capable HTTP server developed by the Apache Software Foundation. It is used to execute special Java programs known as Java Servlet and JavaServer Pages (JSP).

🖥️ Apache Tomcat 9 supports:

🔌 Java Servlet 4.0
💻 JavaServer Pages 2.4
📚 Java Unified Expression Language 3.1
🌐 Java API for WebSocket 2.0 specifications

Note: The major dependency for Apache Tomcat 9.0.x is Java 8 or later. Ensure that Java is installed before downloading and installing Tomcat.

## INSTALL wget COMMAND

sudo yum -y install wget

## Check Java Version

java -version

sudo yum -y install java-11-openjdk java-11-openjdk-devel

## Note: Below Other Command you can try to Install Java

apt install openjdk-11-jre-headless

## Instead, create a dedicated user and group for Tomcat:

sudo groupadd tomcat

sudo useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat

## Create a directory named /opt/tomcat with the mkdir command:

sudo mkdir /opt/tomcat

## DOWNLOAD TOMCAT PACKAGE

export VER="9.0.64"

wget https://dlcdn.apache.org/tomcat/tomcat-9/v${VER}/bin/apache-tomcat-${VER}.tar.gz

curl -O https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.91.tar.gz

## EXTRACT THE DOWNLOADED TAR FILE

sudo tar xvf apache-tomcat-${VER}.tar.gz -C /usr/share/ --strip-components=1

sudo tar xzvf apache-tomcat-9\*tar.gz -C /opt/tomcat --strip-components=1

## Create symlink to extracted tomcat data {This step is not Necessary/Recommended}

sudo ln -s /usr/share/apache-tomcat-$VER/ /usr/share/tomcat

## Assign the tomcat directory ownership to the Tomcat user and group, and ensure the scripts in the bin directory are executable by changing file and directory permissions. Run the following commands for these tasks {Use Anyone as per Your Directory Path}

sudo chown -RH tomcat: /opt/tomcat
sudo chown -R tomcat:tomcat /usr/share/tomcat

sudo chmod +x /opt/tomcat/bin/\*.sh

# The /usr/share/tomcat directory has the following sub-directories:

 bin: contains the binaries and scripts (e.g startup.sh and shutdown.sh f or Unixes and Mac OS X).
 conf : contains the system-wide confguration les,such as server.xml, web.xml, and context.xml.
 webapps: contains the webapps to be deployed. You can alsoplace the WAR (Webapp Archive) le for deployment here.
 lib: contains the Tomcat’s system-wide library JAR les,accessible by all webapps. You could also place external JARle (such as MySQL JDBC Driver) here.
 logs: contains Tomcat’s log les. You may need to check forerror messages here.
 work: Tomcat’s working directory used by JSP, for JSP-to-Servlet conversion

## Determine the Java installation path using the following command:

sudo update-java-alternatives -l

## create a new systemd service file for Tomcat with the following command:

sudo vi /etc/systemd/system/tomcat.service

# Add Below Context in the Above File

[Unit]
Description=Apache Tomcat Web Application Container
After=network.target

[Service]
Type=forking

Environment=JAVA_HOME=/usr/lib/jvm/java-1.21.0-openjdk-amd64
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
Environment=CATALINA_Home=/opt/tomcat
Environment=CATALINA_BASE=/opt/tomcat
Environment=’CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC’
Environment=’JAVA_OPTS.awt.headless=true -Djava.security.egd=file:/dev/v/urandom’

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh

User=tomcat
Group=tomcat
UMask=0007
RestartSec=10
Restart=always

[Install]

WantedBy=multi-user.target

## Save the file and reload the daemon:

sudo systemctl daemon-reload

## start the Tomcat service and check its status with the following systemctl commands:

sudo systemctl start tomcat

sudo systemctl status tomcat

## Now that the Tomcat service is running, you should configure the firewall to allow traffic on port 8080, commonly used by web servers on Ubuntu systems:

sudo ufw allow 8080/tcp

## Add the following line to the file to set up the user and role configurations:

sudo vi /opt/tomcat/conf/tomcat-users.xml

<tomcat-users>

    <role rolename="manager-gui"/>
    <role rolename="admin-gui"/>
    <user username="tomcat" password="P@ssw0rd" fullName="Administrator" roles="manager-gui, admin-gui, admin-script, manager-script, manager-jmx, manager-status"/>

</tomcat-users>
