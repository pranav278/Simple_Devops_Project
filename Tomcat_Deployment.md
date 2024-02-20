
## Setup Jenkins on Amazon Linux Server

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

## Installation of Jenkins on Our Linux Server 

a. sudo su -
6. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4bf635e9-3aa1-45c1-828e-49ae1f0ebb43)

go to this link for installation links : https://pkg.jenkins.io/redhat-stable/
 7. =![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d31b1310-b500-423d-9055-9d601ade9e25)

 b. amazon-linux-extras install epel

 8. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/e8f350cb-3a0c-448b-8b9d-4a5e63c5f7bc)
 check out java installed 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bae4a747-ec48-4ac2-9902-ae5fa0128320)












