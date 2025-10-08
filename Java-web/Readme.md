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
**1**
<img width="1599" height="717" alt="build server" src="https://github.com/user-attachments/assets/3f454725-6026-4e74-8ae5-ed4ffd0d274a" />

**2**
<img width="1238" height="695" alt="SSH connect" src="https://github.com/user-attachments/assets/c0260fa0-bef4-43bf-8e46-465d6449e25b" />

**3**

<img width="557" height="188" alt="change hostname 1" src="https://github.com/user-attachments/assets/ab52633e-de77-49ba-867e-57069a93fc51" />

**4**

<img width="725" height="141" alt="install java 2" src="https://github.com/user-attachments/assets/a7aa17f8-4029-4ffc-a451-83f194944f27" />

**5**

<img width="792" height="217" alt="install maven3" src="https://github.com/user-attachments/assets/47407fa5-a0a4-4266-ae4c-9f8c3cfa7ef6" />

**6**

<img width="963" height="207" alt="git clone 4" src="https://github.com/user-attachments/assets/439d2a0a-9071-4cca-9c7c-aaa36904fbb7" />

**7**

<img width="816" height="166" alt="pom xml file 5" src="https://github.com/user-attachments/assets/31845515-9a07-4ffb-99da-2b3965a7548d" />

**8**

<img width="909" height="432" alt="build success 6" src="https://github.com/user-attachments/assets/8e4977d4-2c5d-4b77-812e-a12ddd0a3ecb" />


On Deploy Server
```
sudo apt update -y
sudo apt install openjdk-11-jdk -y
```
**1**

<img width="1599" height="739" alt="deploy server" src="https://github.com/user-attachments/assets/5762c0e0-1b5e-41b4-9772-932d4ce898e8" />

**2**

<img width="1589" height="571" alt="deploy server SSH" src="https://github.com/user-attachments/assets/4bd488e2-a676-484e-b5c0-5c2ac2e4f28e" />

**3**

<img width="589" height="105" alt="change hostname to deploy-server7" src="https://github.com/user-attachments/assets/57bbae37-19d7-4489-9f99-4d4d0523ffaa" />

**4**

<img width="1598" height="282" alt="install java on deploy server 8" src="https://github.com/user-attachments/assets/5dc48dcf-0ed8-4bbc-a27d-bea48d90d6b3" />


Download and install Apache Tomcat 9:

```

sudo wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.93/bin/apache-tomcat-9.0.93.tar.gz
sudo tar -xvzf apache-tomcat-9.0.93.tar.gz
```
**1**

<img width="1592" height="245" alt="tomcat install 9" src="https://github.com/user-attachments/assets/c5480d12-4ab9-451e-aad1-6603ce89bbf4" />

**2**

<img width="1599" height="713" alt="tomcat 10" src="https://github.com/user-attachments/assets/2884cdf1-48e9-44ef-bdce-5a4412b67b5b" />


🧱 2. Clone the Repository on Build Server
```
git clone https://github.com/AKSarav/TomcatMavenApp.git

cd TomcatMavenApp
```
<img width="963" height="207" alt="git clone 4" src="https://github.com/user-attachments/assets/099a5369-4734-4cce-a2ff-f8758769787d" />

🏗️ 3. Build the WAR File using Maven

```
mvn clean package

```
After build completion, verify that a WAR file is created:

```
ls target/
```
<img width="1293" height="227" alt="unzip and extract 11" src="https://github.com/user-attachments/assets/374e561f-cfae-4f8e-9835-ac8355c358ad" />

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
**1**
<img width="1464" height="519" alt="output" src="https://github.com/user-attachments/assets/caae26db-8c49-4790-adb2-3647cf3d0df1" />


