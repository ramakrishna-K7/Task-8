                                         TASK 8: Run a Simple Java Maven Build Job in Jenkins
________________________________________
STEP 1: Launch EC2 Instance
•	AMI: Amazon Linux Kernel 5.10
•	Instance Type: t2.micro
•	EBS Volume: 8GB
________________________________________
STEP 2:  Install java
sudo yum update -y
sudo amazon-linux-extras enable corretto11
sudo yum install java-11-amazon-corretto -y
# Verify Java
java -version

Install maven
sudo yum install maven -y
# Verify Maven
mvn -version

install jenkins

#STEP-1: INSTALLING GIT 
yum install git  -y

#STEP-2: GETTING THE REPO (jenkins.io --> download -- > redhat)
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

#STEP-3: DOWNLOAD JAVA11 AND JENKINS
yum install java-17-amazon-corretto -y
yum install jenkins -y

#STEP-4: RESTARTING JENKINS (when we download service it will on stopped state)
systemctl start jenkins.service
systemctl status jenkins.service
________________________________________
STEP 3: setup the environment variables
•	Go to the Jenkins dashboard
•	Then go to the manage Jenkins next tools
•	Under jdk installations add jdk
	Name = jdk17
	Java_home = /usr/lib/jvm/java-17-amazon-corretto.x86_64
•	Add maven installations
	Name = mav
	Tick the install automatically
________________________________________
STEP 4: create a job
•	Go to the Jenkins dashboard
•	Click new item setup a name for the project 
•	Select the github project and paste the URL of you GitHub project
•	Under source code management select git, give repository URL and credentials too
•	Under build steps select Invoke top-level Maven targets 
	Version = maven
	Goals = clean package
•	Save the project and build
________________________________________
STEP 4: HelloWorld.java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}

Pom.xml:
<project>
<modelVersion>4.0.0</modelVersion> <groupId>com.example</groupId> <artifactId>hello</artifactId>
<version>1.0</version> <build> <plugins> <plugin> <groupId>org.apache.maven.plugins</groupId> <artifactId>mavencompiler-plugin</artifactId> <version>3.8.1</version> <configuration> <source>1.8</source> <target>1.8</target>
</configuration> </plugin> </plugins> </build> </project>
________________________________________
Output:  
 
![image](https://github.com/user-attachments/assets/a45495b0-e396-4716-8827-3fcc1cfaa54c)


