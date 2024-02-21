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


