## Tomcat Installation & Setup on EC2 Amazon Linux Instance 

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






















