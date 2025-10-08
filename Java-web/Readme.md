# 🚗 Vehicle Management - Java Web Application (Tomcat + Maven)

This project demonstrates how to **build** and **deploy** a Java Web Application using **Apache Maven** and **Apache Tomcat**, with **two separate servers** — one for **build** and one for **deployment**.

---

## 🧩 Project Overview

This is a simple **Java-based web application** that runs on **Tomcat**.  
When deployed successfully, it displays the message:

> **Welcome to Tomcat Maven Application Home Page!**


- One server builds the code using Maven.
- Another server hosts and runs the application on Tomcat.

---

## 🖥️ Architecture

| Role | Server | Description |
|------|---------|-------------|
| 🏗️ Build Server | Maven Build Server | Clones the repository and builds the `.war` file |
| 🚀 Deploy Server | Tomcat Server | Hosts and serves the web application |

---

## ⚙️ 1. Prerequisites

### On Build Server
```
sudo apt update -y
sudo apt install openjdk-11-jdk -y
sudo apt install maven -y
sudo apt install git -y
```
On Deploy Server
```
sudo apt update -y
sudo apt install openjdk-11-jdk -y
```
Download and install Apache Tomcat 9:

```

sudo wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.93/bin/apache-tomcat-9.0.93.tar.gz
sudo tar -xvzf apache-tomcat-9.0.93.tar.gz
```
🧱 2. Clone the Repository on Build Server
```
git clone https://github.com/AKSarav/TomcatMavenApp.git

cd TomcatMavenApp
```
🏗️ 3. Build the WAR File using Maven

```
mvn clean package

```
After build completion, verify that a WAR file is created:

```
ls target/
```
Expected output:

```
TomcatMavenApp.war
```
🔁 4. Transfer the WAR File to the Deploy Server
From the build server, use scp to copy the WAR file to the deploy server:

```
scp target/TomcatMavenApp.war ubuntu@<DEPLOY_SERVER_IP>:/opt/tomcat9/webapps/

Replace <DEPLOY_SERVER_IP> with your actual Deploy Server’s public IP.

```

⚙️ 5. Configure Tomcat on Deploy Server
Step 1: Add a Tomcat User
```

sudo nano /opt/tomcat9/conf/tomcat-users.xml

```
Add this block before </tomcat-users>:

```

<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<user username="admin" password="Admin123" roles="manager-gui,manager-script"/>

```

Step 2: Allow Remote Access to Tomcat Manager
```
sudo nano /opt/tomcat9/webapps/manager/META-INF/context.xml
Comment this line:

```
<!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
           allow="127\.\d+\.\d+\.\d+|::1" /> -->

           
Do the same for:

```
sudo nano /opt/tomcat9/webapps/host-manager/META-INF/context.xml
Comment the same line there too.

```

Step 3: Start Tomcat
```
cd /opt/tomcat9/bin
sudo ./startup.sh
```

To verify Tomcat is running:

```
curl http://localhost:8080

```

You should see Tomcat’s default welcome page HTML.

🌐 6. Access the Deployed Application
Open your browser and visit:

```

http://<DEPLOY_SERVER_IP>:8080/TomcatMavenApp-2.0/
```
If everything is correct, you’ll see:

```

Welcome to Tomcat Maven Application Home Page!

```

