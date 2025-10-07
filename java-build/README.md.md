# 🚀 Java Web Application - Build & Deploy Guide (Java 17 + Maven + Tomcat)

This project demonstrates how to **build and deploy a Java Web Application** using **Java 17**, **Apache Maven**, and **Apache Tomcat**.

---





## 🧱 Part 1: Prerequisites

## Launch two different servers
1. Build server
   
<img width="1599" height="723" alt="build server" src="https://github.com/user-attachments/assets/eaeef248-2089-4866-9716-9d9e4eb250d2" />

2. Deploy server

<img width="1593" height="733" alt="deploy server" src="https://github.com/user-attachments/assets/a11d0201-c4d6-4d97-811b-9bd91cb92c60" />

3. Clone the code in Build server

<img width="906" height="218" alt="git clone 1" src="https://github.com/user-attachments/assets/4a00e3e2-bb77-4ae7-9de8-389d1fbec65a" />

4. update the POM.XML file

<img width="523" height="147" alt="pom xml 1 2" src="https://github.com/user-attachments/assets/9a77a3d3-66a2-48c2-9110-ecab3c32631a" />


<img width="718" height="836" alt="POM XML 2" src="https://github.com/user-attachments/assets/62621c01-a70c-4c93-9fec-f70d94a3e266" />

5. Install maven

<img width="749" height="110" alt="maven install 3" src="https://github.com/user-attachments/assets/72917cf1-d3dd-4023-85fe-d4541d03cb4b" />

6. Maven validate

<img width="809" height="275" alt="mvn validate 4" src="https://github.com/user-attachments/assets/268e7508-cf88-4d1c-80ad-eeb5ab683ee0" />

7. Maven Package

<img width="791" height="262" alt="mvn package 5" src="https://github.com/user-attachments/assets/a27b32d8-e143-4863-a486-ea09578b3fbf" />

8. Warfile

<img width="1449" height="148" alt="war file 6" src="https://github.com/user-attachments/assets/2256a341-9053-4cc4-99fd-89ec4ae5b780" />

9. Connect the Deploy server SSH

<img width="689" height="413" alt="deploy server connect 7" src="https://github.com/user-attachments/assets/7855e108-cdaf-4f73-9231-e94b6c337215" />

10. Install java

<img width="1018" height="193" alt="java install 8" src="https://github.com/user-attachments/assets/977c78e9-2ced-42d2-a092-ae7b9373418d" />

11. Install tomcat

<img width="1599" height="718" alt="tomcat" src="https://github.com/user-attachments/assets/7d528ebe-4414-4d3f-94a1-72bec83b96e3" />

<img width="982" height="232" alt="install tomcat 9" src="https://github.com/user-attachments/assets/18a7e3ea-de66-47db-a37b-438927be946e" />

12. Unzip and extract the file

<img width="519" height="135" alt="unzip and extract 10" src="https://github.com/user-attachments/assets/0e0dcc23-0c68-4732-af28-fb15ccbcd683" />

13. Configure tomcat and restart

<img width="1590" height="511" alt="starting tomcat 11" src="https://github.com/user-attachments/assets/a4eb4f89-15e2-465f-a809-b848b67c311c" />

14. copying pemfile from local to server

<img width="1599" height="476" alt="copying pemfile to server from local" src="https://github.com/user-attachments/assets/09b148e9-a5e2-41b8-8baf-7066b55686e6" />

15. file transfer

<img width="1599" height="253" alt="file transfer 12" src="https://github.com/user-attachments/assets/c3a768b8-5f5b-4472-a4e4-a1fbf8919638" />

16. received file

<img width="1580" height="411" alt="received file 13" src="https://github.com/user-attachments/assets/1cfaa634-51ae-4647-a268-f0ba6ca6dc7e" />

17. Changing user file

<img width="1478" height="504" alt="changing user file 14" src="https://github.com/user-attachments/assets/c7830f6a-61e1-49fa-a878-fafefddaeff8" />

18. output

<img width="736" height="533" alt="output15" src="https://github.com/user-attachments/assets/f46b15cd-ef4a-473e-9198-5501d2ccd282" />










   






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
