# Integrating Tomcat Server in CI/CD

---
Step 1:- Launch Amazon Linux 2 Instance and Connect using Mobaxtrame
Step 2:- Installation of Jenkins on Our Linux Server
Step 3:- Setting Up Jenkins GUI
Step 4:- Installation & Integrate Maven with Jenkins
Step 5:- Tomcat Installation & Setup on EC2 Amazon Linux Instance
Step 6:- Integrate Apache Tomcat with Jenkins
Step 7:- Deploy Artifact On Tomcat Server ( Use of Bash )
---

---
---

## Step 1:- Launch Amazon Linux 2 Instance and Connect using Mobaxtrame

1. **Launch an Amazon Linux 2 Instance**:
   - Log in to the AWS Management Console.
   - Navigate to the EC2 dashboard.
   - Click on "Launch Instance" and choose "Amazon Linux 2 AMI".
   - Follow the steps in the instance launch wizard, select your instance type, configure instance details, add storage, configure security groups, and review.
   - When configuring the security group, create a new security group with the necessary rules (HTTP, HTTPS, SSH).

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0ef2d7b9-7b04-438c-a454-1ced049ad711)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/8a4cfc23-b1d9-4e87-9f68-2aa82d4b8c60)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bc25a35a-0554-4ae7-bdde-c189cb86a913)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/b0964de4-769d-4123-ad28-8d52c0300407)


2. **Connect to your Amazon Linux instance using MobaXterm**

   1. **Download and Install MobaXterm**:
   - If you haven't already, download and install MobaXterm from the official website: [MobaXterm](https://mobaxterm.mobatek.net/download.html).

   2. **Launch MobaXterm**:
   - Open MobaXterm from your desktop or start menu.

   3. **Open a New SSH Session**:
   - Click on the "Session" button in the upper-left corner.
   - Select "SSH" as the session type.

   4. **Configure SSH Session**:
   - In the "Remote host" field, enter the public IP address of your Amazon Linux instance.
   - In the "Specify username" field, enter `ec2-user`.
   - In the "Advanced SSH settings" section, click on the "Use private key" checkbox and select your PEM key file by clicking on the file icon.
   - Optionally, you can set the port to `22` if it's different from the default SSH port.
   - Click "OK" to save the session settings.

   5. **Connect to the Instance**:
   - Double-click on the session you just configured, or select it and click "Start session".

   6. **Authenticate**:
   - If prompted, confirm any security messages about connecting to a new host.
   - MobaXterm should now establish an SSH connection to your Amazon Linux instance using the provided credentials and PEM key.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4ea0ee84-ddb0-4a83-914c-494e1e76559a)

Once Login you will see this console

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/936e1c03-8f4f-45da-9093-976ff9078f3b)

---









---

## Step 2:- Installation of Jenkins on Our Linux Server
   
1. To switch to the root user, you can use the 'sudo su -' command. This command essentially elevates your privileges to root, allowing you to execute commands as the root user.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4bf635e9-3aa1-45c1-828e-49ae1f0ebb43)

2. Go to this link for installation links : https://pkg.jenkins.io/redhat-stable/

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d31b1310-b500-423d-9055-9d601ade9e25)

3. To install the EPEL (Extra Packages for Enterprise Linux) repository on an Amazon Linux instance, you can use the `amazon-linux-extras` command. Here are the steps:

1. Connect to your Amazon Linux instance via SSH using MobaXterm or any other SSH client.

2. Switch to the root user by running:

```
sudo su -
```

3. Install the EPEL repository using the `amazon-linux-extras` command:
```
amazon-linux-extras install epel
```

4. After running the command, it will prompt you to confirm the installation. Type `y` and press Enter to proceed with the installation.


- Now you have successfully installed the EPEL repository on your Amazon Linux instance. You can now use it to install additional packages available in the EPEL repository using the `yum` package manager.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/e8f350cb-3a0c-448b-8b9d-4a5e63c5f7bc)
 
       
5. Check out java installed 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bae4a747-ec48-4ac2-9902-ae5fa0128320)
       
- Here we see java is not present so we need to install

6. To install the Java OpenJDK 11 package on an Amazon Linux system using the Amazon Linux Extras feature
```
amazon-linux-extras install java-openjdk11
```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6feccc3a-0226-4d7e-931a-588a9c1b137f)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4c583822-fece-4162-841f-4397213bf8f6)
      
7. insatll jenkins
```
yum install jenkins
```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f1016f9a-69b2-460c-a799-acc4c5a39692)
      
8. Now check the status of Jenkins
 ```
 service jenkins status
 ```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/fc2535b7-c01d-4e65-9d38-4ab5ab48da49)
      
9. Start the Jenkins
```
service jenkins start
```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/73a7c66b-bdcd-4ffb-a1cb-35edbead01f4)
      
10. Go to the Security Group of Jenkins and Allow 8080 inbound rule

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/67ad246e-1f2a-442e-8fa4-0169a9833e91)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/9ce70d5e-5c36-4287-b861-d5c1f0587987)

11. Now access the Jenkins by hitting the Public ip on web Browser

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/45fd74cd-8829-4582-8a81-57a5461de8a6)

---




---
## Step 3:- Setting Up Jenkins GUI

The password for Jenkins is typically not stored in a specific file path like other configurations. Instead, Jenkins manages user authentication using its own user database or an external authentication provider.

However, if you're referring to the Jenkins admin password, which is initially generated during the Jenkins setup wizard, it is usually stored in the Jenkins home directory in a file named `secrets/initialAdminPassword`.

```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```

After retrieving the initial admin password, you can use it to log in to Jenkins for the first time and set up your admin user Account 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/74b16420-2a88-4657-8b31-2f7ab60454c7)
     
 
After entering Password Click on Continue and We dont need any Plugins currently so Cancel it 
      
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/b4d8cdbd-c875-46ff-99b3-0e81c7d9baa4)

We can  See now Jenkins Home Page
      
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/83703df6-4d65-4a66-b612-8370cd9d5b14)

## **Integrate Github with Jenkins**
      1. Install Git on Jenkins Instance
      2. Install Github Plugin on Jenkins GUI
      3. Configure Git on Jenkins GUI

1. Install Git on Jenkins Instance
   1. Check Git Installed or Not
   ```
   git
   ```
   ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a7e375b4-c765-4f64-9699-a3ee7e6500cb)

   2. Install Git
   ```
   yum install git
   ```
   ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d4a05786-a863-4bb2-914d-882027bfba55)

## Install Github Plugin on Jenkins GUI

To install the GitHub Plugin and configure Git installation in Jenkins, follow these steps:

### Install GitHub Plugin:

1. Navigate to your Jenkins dashboard.
2. Click on "Manage Jenkins" in the left sidebar.
3. Select "Manage Plugins" from the dropdown menu.
4. Go to the "Available" tab.
5. Use the search box to search for "GitHub".
6. Check the checkbox next to "GitHub Plugin".
7. Click on the "Install without restart" button.

### Add Git Installation Configuration:

1. After installing the GitHub Plugin, go back to the "Manage Jenkins" page.
2. Select "Global Tool Configuration" from the list.
3. Scroll down to the "Git installations" section.
4. Click on "Add Git" to add a new Git installation.
5. Enter the following details:
   - **Name:** git
   - **Path to Git executable:** Enter the path to the Git executable. If Git is installed globally, you can usually leave this field empty as Jenkins will search for Git in the system's PATH.
6. Click on "Save" to save the configuration.

Now, Jenkins is configured with the GitHub Plugin and Git installation. You can use Git in your Jenkins jobs for version control and integrate with GitHub repositories.
  
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0018a7e7-56dd-455d-8a0b-15797eee0474)
      
Click on Install without Restart
   
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5f62e98a-47ed-47a8-b022-032ea27502e0)


Click on Apply and SAVE
---




---
## Step 4:- Installation & Integrate Maven with Jenkins


      1. Setup Maven on Jenkins Server
      2. Setup Environment Variables ( JAVA_HOME, M2, M2_HOME )
      3. Install Maven Plugin
      4. Configure Maven And Java


To navigate to the `/opt` directory and then install Maven from a tar.gz archive, follow these steps:

1. **Navigate to the `/opt` Directory:**
   Open a terminal and use the `cd` command to navigate to the `/opt` directory:

   ```bash
   cd /opt
   ```

2. **Download Maven:**
   You can download the latest version of Maven directly to the `/opt` directory using `wget` or `curl`. For example, using `wget`:

   ```bash
   wget https://downloads.apache.org/maven/maven-3.x.x/binaries/apache-maven-3.x.x-bin.tar.gz
   ```

   Replace `3.x.x` with the latest version number available.

3. **Extract the Archive:**
   Once the download is complete, extract the Maven archive using the `tar` command:

   ```bash
   tar -xvzf apache-maven-3.x.x-bin.tar.gz
   ```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f5d06644-ee14-4f6f-a13d-cdcae0424096)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/9e9899a0-e839-452b-b0f9-fbb50acbe4c2)

* Moved that file to the maven dir
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/853b0024-ca7f-4c32-b70f-50afd5a0158e)

* If the `mvn` command is not found, it indicates that Maven's bin directory is not included in the system's PATH environment variable. To fix this issue, you need to ensure that the PATH environment variable includes the bin directory of the Maven installation.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/7badc669-6ac5-4de8-83c2-21fae03e49cb)

If you're using Bash as your shell, you can set environment variables in the ~/.bash_profile file. This file is executed for login shells, and it's a common place to set environment variables on Unix-like systems

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d13ac34b-bff4-4a61-b3ee-27f3c977ddd6)

* **Set M2_HOME, M2, and JAVA_HOME:**
   Add the following lines to set the environment variables:

   ```bash
   export M2_HOME=/opt/maven
   export M2=$M2_HOME/bin
   export JAVA_HOME=/path/to/java
   ```

   Replace `/opt/maven` with the actual path to your Maven installation directory and `/path/to/java` with the actual path to your Java installation directory.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/16569790-6d2f-4668-88b1-914c1e0c99bb)

* To find the Java path on your system, you can use the `find` command to search for the directory containing `jvm` executable. Here's how you can do it:

```bash
sudo find /  -name jvm
```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/87546095-e8f7-4865-8932-671fa652ceb2)

* Check the Changes are Affected or not
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f9fb65b5-6ad4-4fb9-b828-2126cce48e35)

* After making changes to your `.bash_profile` or `.bashrc` file, you need to reload it to apply the changes. You can do this using the `source` command. Here's how:

```bash
source ~/.bash_profile
```


```
source .bash_profile
```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bb124730-4675-49ea-a847-3ea9c7cc54b3)

* Now MVN execute from Anywhere

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/9a5d972c-e1a4-4918-8d39-6037c1d463d5)

To add the Maven Integration Plugin and configure Java and Maven tools in Jenkins, you can follow these steps:

1. **Add Maven Integration Plugin:**
   - Navigate to your Jenkins dashboard.
   - Click on "Manage Jenkins" in the left sidebar.
   - Select "Manage Plugins" from the dropdown menu.
   - Go to the "Available" tab.
   - Use the search box to search for "Maven Integration".
   - Check the checkbox next to "Maven Integration" plugin.
   - Click on the "Install without restart" button.

2. **Configure Java and Maven Tools:**
   - After installing the Maven Integration Plugin, go back to the "Manage Jenkins" page.
   - Select "Global Tool Configuration" from the list.
   - Scroll down to the "JDK installations" section.
   - Click on "Add JDK" to add a new JDK installation.
   - Enter the following details:
     - Name: Java11
     - JAVA_HOME: Provide the path to your JDK installation directory for Java 11.
   - Click on "Save" to save the configuration.

   - Scroll down to the "Maven installations" section.
   - Click on "Add Maven" to add a new Maven installation.
   - Enter the following details:
     - Name: Maven3
     - MAVEN_HOME: `/opt/maven` (or the path to your Maven installation directory).
   - Click on "Save" to save the configuration.

Now, Jenkins is configured with the Maven Integration Plugin, and Java and Maven tools are set up. You can use these tools in your Jenkins jobs to build and test Maven projects.
 
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4fa2ebd8-203d-4294-bc95-32d72d3c85e7)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2b4bbba2-6b43-46a9-88bd-4619dfd8e46f)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f5fcabb4-89a6-4a9d-a52e-a90fb53950c6)

---




---
## Step 5:- Tomcat Installation & Setup on EC2 Amazon Linux Instance

1. **Sign in to AWS Console:**
   Go to the AWS Management Console (https://aws.amazon.com/console) and sign in to your AWS account.

2. **Open EC2 Dashboard:**
   Once logged in, navigate to the EC2 dashboard by clicking on the "Services" dropdown menu at the top-left corner, then selecting "EC2" under the "Compute" section.

3. **Launch Instance:**
   Click on the "Launch Instance" button to start the process of launching a new EC2 instance.

4. **Choose AMI:**
   In the "Step 1: Choose an Amazon Machine Image (AMI)" section:
   - Select "AWS Marketplace" on the left sidebar.
   - Search for "Amazon Linux 2" in the search bar.
   - Select the appropriate Amazon Linux 2 AMI from the search results.

5. **Choose Instance Type:**
   In the "Step 2: Choose an Instance Type" section, select the instance type that meets your requirements. For example, you can choose a t2.micro instance type for a basic setup.

6. **Configure Instance:**
   Proceed to the Default 

7. **Add Storage:**
   In the "Step 4: Add Storage" section, you can specify the size of the root volume (usually the default is fine for most cases).

8. **Add Tags (Optional):**
   In the "Step 5: Add Tags" section, you can add tags to your instance for better organization. Tags are key-value pairs that you can use to categorize your instances.

9. **Configure Security Group:**
   In the "Step 6: Configure Security Group" section:
   - Create a new security group by selecting "Create a new security group" option.
   - Set the security group name and description.
   - For the inbound rules, add a rule that allows all traffic (source: 0.0.0.0/0, ::/0, or anywhere) for all protocols and all ports.
   - For the outbound rules, keep the default settings which allow all traffic.

10. **Review Instance Launch:**
    Review all your configurations in the "Step 7: Review Instance Launch" section. If everything looks good, click on the "Launch" button.

11. **Select Key Pair:**
    You will be prompted to create a new key pair or select an existing one. Choose "Create a new key pair", enter a name for the key pair, and then click "Download Key Pair". Make sure to store the downloaded private key (.pem file) in a secure location as it will be required to access your instance.

12. **Launch Instances:**
    After downloading the key pair, click on the "Launch Instances" button. Connect using Mobaxtrame 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f0c10770-e35d-4406-81c5-d5fbde40f66a)

To install Java 11 on an Amazon Linux AMI 2 instance, you can use the `amazon-linux-extras` command. Here's the command you can run after switching to the root user:

```bash
amazon-linux-extras install java-openjdk11
```

Here's what each part of the command does:

- `amazon-linux-extras`: This is a command-line tool provided by Amazon Linux that allows you to enable, disable, and install additional software repositories (known as "extras").
- `install`: This subcommand is used to install the specified extra.
- `java-openjdk11`: This is the name of the extra package that provides OpenJDK 11, which is Java 11.

After running this command, Java 11 will be installed on your Amazon Linux AMI 2 instance, and you can verify the installation by running:

```bash
java -version
```

This should display the version of Java installed on your system, confirming that Java 11 is now available.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2771b9ab-8eb1-4a4b-b36a-ccb8e3f31cbb)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6aac289e-30ad-426f-8a3e-0f59d5d70f60)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5ec37763-cc76-4a69-b46e-27b8b68d7eb9)

To install Apache Tomcat 8 on your server inside the /opt directory using the tar.gz file from the official Tomcat page, you can follow these steps:

1. **Download Tomcat:**
   First, navigate to the official Apache Tomcat website (https://tomcat.apache.org/download-80.cgi) and download the latest version of Tomcat 8 as a tar.gz file. You can use `wget` or `curl` commands to download the file directly to your server.

   ```bash
   wget https://downloads.apache.org/tomcat/tomcat-8/v8.x.x/bin/apache-tomcat-8.x.x.tar.gz
   ```


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a9885cc6-28c2-4d51-affa-f463987f07b2)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/78493f9d-fb52-40fc-80d2-b81fa1bc495e)

2. **Extract Tarball:**
   Once the download is complete, extract the tar.gz file to the desired installation directory.

   ```bash
   tar -xzvf apache-tomcat-8.x.x.tar.gz 
   ```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c31f9811-0f05-4175-a960-6446f5a936b3)

3. **Rename Directory (Optional):**
   If you want, you can rename the extracted directory for convenience.

   ```bash
   mv /opt/apache-tomcat-8.x.x  tomcat
   ```
   
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/107c63dc-83e9-4b1c-9199-99e32aabcd37)

1. **Navigate to the Tomcat Installation Directory:**

```bash
cd /opt/tomcat
```

This command changes the current directory to the Tomcat installation directory. Replace `/opt/tomcat` with the actual path to your Tomcat installation directory if it's different.

2. **Start Tomcat:**

```bash
./startup.sh
```

This command executes the startup script (`startup.sh`) located in the `bin` directory of the Tomcat installation directory. The `./` before `bin/startup.sh` indicates that the script is located in the current directory.

3. **Stop Tomcat:**

```bash
./shutdown.sh
```


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6198bf50-fc90-43de-a670-dcd39edf5f30)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/407c6efc-9eb6-4190-8711-7dc11f66324f)

To verify that Tomcat is running and accessible from a web browser, you can follow these steps:

1. **Open a Web Browser:**
   Open any web browser of your choice on your local machine.

2. **Enter Tomcat URL:**
   Enter the URL of your Tomcat server in the address bar of the web browser. By default, Tomcat listens on port 8080. If your server's IP address is `your_server_ip`, then the URL would be:

   ```
   http://your_server_ip:8080
   ```

   Replace `your_server_ip` with the actual IP address or hostname of your server.
   

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/ff502ed7-3ba4-4e68-9abb-00adfb6fe870)

The `context.xml` file in Apache Tomcat typically resides within the configuration directory of a specific web application. This file allows you to define settings and resources for a web application, such as data sources, security constraints, and environment entries

You can use the `find` command to search for the `context.xml` file within the Tomcat directory structure. Here's how you can do it:

```bash
find / -name "context.xml"
```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/92a062fd-2554-4b00-9653-a45b7ea55038)

Modify the Below changes using Vi Editor 

*RemoteAddrValve Configuration** (`server.xml`):
   ```xml
   <!--
   <Valve className="org.apache.catalina.valves.RemoteAddrValve"
          allow="127\.\d+\.\d+\.\d+|::10:0:0:0:0:0:0:1" />
   -->
   ```
   This snippet configures the `RemoteAddrValve`, which is a Valve responsible for filtering requests based on the remote IP address. In this configuration:
   - `className`: Specifies the class responsible for filtering requests based on remote IP addresses.
   - `allow`: Specifies a regular expression pattern for IP addresses to allow. In this case, it allows requests from `127.x.x.x` and `::10:0:0:0:0:0:0:1`, which are typically localhost addresses.

* So far accessing command out these things

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6068b8fb-8937-443e-9470-6c499bcc2227)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c5fc893e-05c0-40b9-a272-b6994442b422)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/51fbd8bb-4322-48a6-9d33-574b0899e104)


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f2c97861-5a60-40ad-b6aa-d3c2277a538f)

* After Modificaion need to restart tomcat service 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d81699d8-8228-498a-8dd9-e7c73dbfb080)

* Now verify Tomcat ask for user Credentials 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a1d100b0-d713-4650-aa15-76ae7c9b3186)

The `tomcat-users.xml` file in Apache Tomcat is used to configure users and roles for accessing the Tomcat Manager and Host Manager web applications. This file defines usernames, passwords, and associated roles that control access to these applications.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/b11e11fc-88e6-4eaf-b9ff-b309539de2d0)

Update users information in the tomcat-users.xml file goto tomcat home directory and Add below users to conf/tomcat-users.xml file
```
 <role rolename="manager-gui"/>
 <role rolename="manager-script"/>
 <role rolename="manager-jmx"/>
 <role rolename="manager-status"/>
 <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
 <user username="deployer" password="deployer" roles="manager-script"/>
 <user username="tomcat" password="s3cret" roles="manager-gui"/>
```

These lines define three users:

- `admin`: Has access to all roles defined (`manager-gui`, `manager-script`, `manager-jmx`, `manager-status`), typically used for administrative purposes.
- `deployer`: Has access only to the `manager-script` role, typically used for deploying applications via scripts.
- `tomcat`: Has access only to the `manager-gui` role, typically used for accessing the HTML interface of the Tomcat Manager application.


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6189bc96-1ac0-4d40-aa52-f00cf15ae54e)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2084b072-f396-4fc3-b28d-61d79047bce4)

This configuration allows different users to have different levels of access to the Tomcat Manager and related interfaces, depending on their roles.


To simplify the process of starting and stopping Tomcat by creating symbolic links for the `startup.sh` and `shutdown.sh` scripts, you can follow these steps:

1. **Navigate to the Directory Where You Want to Create the Links:**
   Choose a directory where you want to create the symbolic links. For example, you might choose a directory that's already in your system's `PATH` environment variable so you can execute the commands from anywhere.

   ```bash
   cd /usr/local/bin
   ```

   Replace `/usr/local/bin` with the directory of your choice.

2. **Create Symbolic Links:**
   

   This creates symbolic links named `tomcat-start` and `tomcat-stop` in the current directory that point to the respective scripts in the Tomcat installation directory.
```

ln -s /opt/apache-tomcat-<version>/bin/startup.sh /usr/local/bin/tomcatup
ln -s /opt/apache-tomcat-<version>/bin/shutdown.sh /usr/local/bin/tomcatdown
```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/361d91ec-df00-4a4b-b4f4-74c5d38098f2)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/119c8da3-f8d1-495f-b9c6-c5c0a28c0b61)

* Tomcat is working by Using Symbolic link also

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/65f9558c-3375-4fd5-bd86-2ec69270ae77)
---




---
## Step 6:- Integrate Apache Tomcat with Jenkins


Integrating Apache Tomcat with Jenkins allows you to deploy Java web applications directly from Jenkins to Tomcat servers. Here's a basic outline of the integration process:

Add the "Deploy to Container Plugin" in Jenkins:

1. **Open Jenkins Dashboard:**
   Open your web browser and navigate to your Jenkins server's URL. Log in to the Jenkins dashboard with your credentials.

2. **Go to Manage Jenkins:**
   Click on "Manage Jenkins" from the left-hand sidebar. This will take you to the Jenkins management page.

3. **Access Plugin Manager:**
   In the "Manage Jenkins" page, click on "Manage Plugins." This will open the Jenkins Plugin Manager.

4. **Navigate to Available Plugins:**
   In the Plugin Manager, you'll find different tabs. Click on the "Available" tab to view the list of available plugins that can be installed.

5. **Search for "Deploy to Container Plugin":**
   In the search box, type "Deploy to Container Plugin" or simply "Deploy to Container". The plugin should appear in the filtered list.

6. **Select Plugin for Installation:**
   Find the "Deploy to Container Plugin" in the list of available plugins and check the checkbox next to it.

7. **Install Plugin:**
   After selecting the "Deploy to Container Plugin", scroll down to the bottom of the page and click on the "Install without restart" button. This will begin the installation process.

8. **Wait for Installation:**
   Jenkins will download and install the plugin. This may take a few moments depending on your network speed and server performance.

9. **Verify Installation:**
   Once the installation is complete, you'll see a message indicating that the plugin was installed successfully.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/3c371208-d207-452d-b33e-913dbb27c793)

To configure Tomcat credentials in Jenkins using the Global Credentials feature, follow these steps:

1. **Access Jenkins Dashboard:**
   Log in to your Jenkins server and navigate to the Jenkins dashboard.

2. **Go to Manage Jenkins:**
   Click on "Manage Jenkins" from the sidebar menu. This will take you to the management page.

3. **Access Credentials:**
   In the "Manage Jenkins" page, click on "Manage Credentials". This will open the Credentials page where you can manage various types of credentials.

4. **Add Global Credentials:**
   In the Credentials page, click on "Global credentials (unrestricted)" from the left-hand side menu.

5. **Add Credentials:**
   Click on the "Add Credentials" link to add a new credential.

6. **Select Credentials Kind:**
   Choose the type of credentials you want to add. Since you're adding Tomcat credentials, you might select "Username with password".

7. **Enter Credentials Information:**
   Fill in the following details:
   - **Username:** Enter the username for the Tomcat user (e.g., `deployer`).
   - **Password:** Enter the password for the Tomcat user (e.g., `deployer`).
   - **ID:** Optionally, you can specify an ID for the credentials. This ID is used to reference the credentials in Jenkins configurations.

8. **Scope Configuration:**
   Set the appropriate scope for the credentials. Since you want to use these credentials globally, you should leave the scope as "Global (Jenkins, nodes, items, all child items, etc)".

9. **Click on "OK" or "Create":**
   After entering the required information, click on "OK" or "Create" to save the credentials.

10. **Verify Credentials:**
    Once you've created the credentials, you can verify that they appear in the list of global credentials. You should see the credentials you just added listed there.

By configuring Tomcat credentials in Jenkins using the Global Credentials feature, you can securely manage authentication information for Tomcat servers and use them in your Jenkins jobs for deploying applications or performing other tasks.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/97af7c58-be2d-4f9e-b774-0532d1c36184)

c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/3ad897ba-3b4e-4953-948f-8946f8e5ff2b)

d. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bb374b41-230e-46b4-bb77-9c0856475df9)

To create your first Maven job in Jenkins for deploying a project, named "Deployment of Job", follow these steps:

1. **Access Jenkins Dashboard:**
   Log in to your Jenkins server and navigate to the Jenkins dashboard.

2. **Create a New Job:**
   Click on the "New Item" or "New Job" link on the Jenkins dashboard. This will start the process of creating a new job.

3. **Enter Job Details:**
   - Enter the name "Deployment of Job" in the "Enter an item name" field.
   - Select "Maven Project" as the project type.
   - Click "OK" to proceed.

4. **Configure Maven Project:**
   You will be directed to the configuration page for the Maven project. Here's how to configure it:

   - **General:**
     - Description: (Optional) Add a description for your Maven job.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/41ab6fb1-1440-4117-8ff7-f6022ddeb219)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a66c84b4-fa84-4f02-bb7b-d2b813e4938b)

5. **Configure Source Code Management:**
   Scroll down to the "Source Code Management" section.

6. **Choose Git:**
   Select "Git" as the source code management system. This will reveal options specific to configuring Git.

7. **Add Repository URL:**
   In the "Repository URL" field, enter the URL of your Git repository.

8. **Leave Credentials Empty:**
   Since your Git repository is public and doesn't require credentials, leave the "Credentials" field empty. Jenkins will automatically handle authentication for public repositories.

9. **Branches to Build (Optional):**
   If you want to build specific branches, you can specify them in the "Branches to build" field. Otherwise, Jenkins will build the default branch (usually `master`).

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5584bbd0-22eb-48b1-b959-20a96c11ed09)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f6743744-54a0-4396-bc6c-e2af588b5ba7)

10. **Configure Build Environment:**
   Scroll down to the "Build" section and click on the "Add build step" dropdown.

11. **Set Root POM:**
   In the "Root POM" field, enter the path to your `pom.xml` file. If your `pom.xml` file is located in the root directory of your project, you can simply enter `pom.xml`.

12. **Set Goals and Options:**
   In the "Goals and options" field, enter the Maven goals and options you want to execute during the build process. For example, you can enter `clean install` to clean the project and then install dependencies and package the project into a JAR or WAR file.

By configuring the build environment with the specified `pom.xml` file and Maven goals and options, Jenkins will execute the Maven build according to your project's requirements. This setup allows for flexibility in configuring the Maven build process within Jenkins.
   
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/71a5d067-ea3c-436d-8dcd-164ad8f98884)

To configure Jenkins to deploy the WAR files to a remote Tomcat server as a post-build action, follow these steps:

1. **Access Jenkins Dashboard:**
   Log in to your Jenkins server and navigate to the Jenkins dashboard.

2. **Select Your Maven Project:**
   Click on the "Deployment of Job" Maven project you've created to edit its configuration.

3. **Configure Post-Build Actions:**
   Scroll down to the "Post-build Actions" section.

4. **Add Post-Build Action:**
   Click on the "Add post-build action" dropdown and select "Deploy war/ear to a container".

5. **Specify WAR File:**
   - In the "WAR/EAR files" field, enter `**/*.war`. This specifies that Jenkins should deploy all WAR files found in the project workspace.

6. **Set Context Path:**
   - Leave the "Context path" field blank. This means that Tomcat will use the default context path for the deployed application.

7. **Select Tomcat Container:**
   - Choose "Tomcat 8.x Remote" from the "Containers" dropdown. This specifies that Jenkins will deploy the WAR files to a remote Tomcat server.

8. **Specify Tomcat Credentials:**
   - In the "Credentials" dropdown, select the credentials you created earlier for authenticating with the Tomcat server.

9. **Enter Tomcat URL:**
   - In the "Tomcat URL" field, enter the URL of your Tomcat server where you want to deploy the WAR files (e.g., `http://your_tomcat_server:8080`). Make sure to replace `your_tomcat_server` with the actual hostname or IP address of your Tomcat server.

10. **Save Configuration:**
    Once you've configured the post-build actions, click on the "Save" or "Apply" button to save the changes.

11. **Run the Job:**
    You can now run the Maven job by clicking on the "Build Now" button. Jenkins will start the build process and deploy the WAR files to the specified Tomcat server as a post-build action.

By following these steps, Jenkins will automatically deploy the WAR files to the remote Tomcat server after a successful build, streamlining the deployment process for your Maven project.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d0b4c026-ce1e-43ed-b4c1-02c6e7618af7)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c5c74416-c8b2-4641-a673-4979783071e9)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2c150f51-2252-4359-a9f3-c4f0707d53ea)

Once the Jenkins job runs and successfully deploys the WAR file to the Tomcat server, you should be able to see the deployed application listed in the Tomcat Web Application Manager.

To access the Tomcat Web Application Manager:

1. Open a web browser and navigate to the Tomcat Manager URL. This is typically `http://your_tomcat_server:8080/manager/html`.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/82d7ba7a-c18a-4f9e-9308-56c606cec5e1)

* Output :- 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/738c777a-3633-483e-9a8a-16708f2fab36)

---




---
## Step 7:- Deploy Artifact On Tomcat Server ( Use of Bash )

Open Git Bash on your local machine. You can usually find it in the Start menu on Windows or by searching for "Git Bash".

You should be able to clone a project, make changes, and push those changes to a remote repository using Git Bash on your local machine.

1. **Navigate to Your Desired Location:**
   Use the `cd` command to navigate to the directory where you want to clone the project. For example:
   ```bash
   cd /path/to/your/directory
   ```

2. **Clone the Project:**
   Use the `git clone` command to clone the project from the remote repository. Replace `<repository_url>` with the URL of the remote repository:
   ```bash
   git clone <repository_url>
   ```

3. **Navigate into the Cloned Directory:**
   Use the `cd` command to navigate into the cloned directory:
   ```bash
   cd <cloned_project_directory>
   ```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/00b147f6-9970-47c8-9647-7effeb7b1af3)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/501d96ba-37e6-4cc0-bb42-61e76d205551)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/1cce9758-b6d0-4d4c-9f01-ea05a0c853c1)

4. Use the `cd` command to change directory to the `webapps` directory. If you're unsure of the exact path, you can use the `find` command to locate it. Assuming Tomcat is installed in the default location on Linux, you might run:

   ```bash
   cd /var/lib/tomcat/webapps
   ```

   Replace `/var/lib/tomcat8/webapps` with the actual path to your `webapps` directory if it's different.

5. Once inside the `webapps` directory, you can locate the `index.jsp` file and make changes to it using your preferred text editor. For example, you might run:

   ```bash
   vi index.jsp
   ```


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0335bc09-da09-4a45-a65e-9df873520fcd)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c07c83fe-2513-432f-b8f8-4d72765a1f4b)

If you've made changes to files in your project directory and you want to check the status of these changes using Git, you can use the `git status` command. Here's how you can do it:

1. Once you're in your project directory, run the following command to check the status of your changes:

   ```bash
   git status
   ```

   This command will show you the current state of your working directory, including any changes that have been made to files, untracked files, and the branch you're currently on.

2. Look for the `index.jsp` file in the list of modified files. It should appear under the "Changes not staged for commit" section.

3. If you want to stage the changes to be included in the next commit, you can use the `git add` command followed by the filename. For example, to stage changes to `index.jsp`, you would run:

   ```bash
   git add index.jsp
   ```

4. After staging the changes, you can commit them using the `git commit` command. For example:

   ```bash
   git commit -m "Updated index.jsp with changes"
   ```

   Replace the commit message with an appropriate description of the changes you've made.

5. Finally, you can push the changes to your remote repository using the `git push` command. For example:

   ```bash
   git push origin <branch-name>
   ```

By following these steps, you can check the status of your changes, stage them for commit, commit them to your local repository, and push them to your remote repository using Git.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/122cc2e9-0efe-4fc4-9c5b-ca2807f0cdf3)


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/1990f88c-6b29-4b0d-a12b-367c4fa872c8)


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2fbc2fce-49c9-48f7-a49b-7d49a3e4735d)


Replace `<branch-name>` with the name of the branch you want to push your changes to, typically `master` or `main`.
   












































