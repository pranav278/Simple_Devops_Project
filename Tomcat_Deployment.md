
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

























