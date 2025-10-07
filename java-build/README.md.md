# 🚀 Java Web Application - Build & Deploy Guide (Java 17 + Maven + Tomcat)

This project demonstrates how to **build and deploy a Java Web Application** using **Java 17**, **Apache Maven**, and **Apache Tomcat**.

---





## 🧱 Part 1: Prerequisites

### ✅ Install Java 17
```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```
✅ Install Apache Maven
```

sudo apt install maven -y
mvn -v
```

✅ Install Apache Tomcat 9
```
wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.85/bin/apache-tomcat-9.0.85.tar.gz
tar -xvzf apache-tomcat-9.0.85.tar.gz
sudo mv apache-tomcat-9.0.85 /opt/tomcat
cd /opt/tomcat/bin
./startup.sh
Access Tomcat at:
👉 http://localhost:8080
```
## ⚙️ Part 2: Tomcat Configuration
✅ Add Tomcat User
Edit tomcat-users.xml:

```
sudo nano /opt/tomcat/conf/tomcat-users.xml
```

xml
Copy code
```
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<user username="admin" password="admin123" roles="manager-gui,manager-script"/>
```
✅ (Optional) Allow Remote Access
Edit:

```
sudo nano /opt/tomcat/webapps/manager/META-INF/context.xml
```
Comment out the restriction:

xml
Copy code
```
<!--
<Valve className="org.apache.catalina.valves.RemoteAddrValve"
       allow="127\.\d+\.\d+\.\d+|::1" />
-->
```
Restart Tomcat:

```
/opt/tomcat/bin/shutdown.sh
/opt/tomcat/bin/startup.sh
```
## 🛠️ Part 3: Build the WAR File
✅ Update pom.xml
xml
```
<properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>

<packaging>war</packaging>
```
✅ Build Using Maven
```
cd JavaWebCalculator
mvn clean package
Your WAR file will be generated at:
target/webapp-0.2.war
```

## 🚀 Part 4: Deploy to Tomcat
✅ Option 1: Deploy via Manager Interface
Go to:
```

👉 http://localhost:8080/manager/html
Login → Upload the WAR file → Click Deploy

```

Access at:
```
👉 http://localhost:8080/webapp-0.2

```

✅ Option 2: Deploy via File Copy
```

cp target/webapp-0.2.war /opt/tomcat/webapps/

```
Tomcat auto-deploys it.

🧪 Part 5: Verify Deployment
Visit:

```

http://localhost:8080/webapp-0.2/

```
Tail Tomcat logs:

```

tail -f /opt/tomcat/logs/catalina.out

```

## 🧩 Author
**Name:** Pawankumar Kothapalli
DevOps & Cloud Enthusiast ☁️
📍 Hyderabad, India