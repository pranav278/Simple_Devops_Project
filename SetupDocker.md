


1. **Login to AWS Console**: Go to the AWS Management Console and login to your AWS account.

2. **Navigate to EC2 Dashboard**: Go to the EC2 dashboard by selecting "Services" from the top navigation bar, then clicking on "EC2" under the Compute section.

3. **Launch Instance**:
   - Click on the "Launch Instance" button.
   
4. **Choose AMI**:
   - Select "Amazon Linux 2 AMI" from the list of available AMIs.

5. **Choose Instance Type**:
   - Select an instance type based on your requirements. For example, you can choose t2.micro, which falls under the Free Tier.

6. **Configure Instance Details**:
   - Leave the default settings or configure as per your requirements.

7. **Add Storage**:
   - Configure the storage as per your requirements.

8. **Add Tags**:
   - Optionally, you can add tags to your instance for better organization.

9. **Configure Security Group**:
   - Create a new security group or select an existing one. Ensure that you allow all traffic (0.0.0.0/0) for all ports for simplicity, but for production systems, you should restrict access based on your needs.

10. **Review Instance Launch**:
    - Review the configuration to ensure everything is set up correctly.

11. **Generate Key Pair**:
    - In the "Key Pair" section, select "Create a new key pair" from the drop-down menu.
    - Enter a name for your key pair, for example, "docker-server-key-pair".
    - Click on "Download Key Pair" to save the .pem file to your local machine.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/e3157e56-610d-4112-ab02-1228185bb082)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/81987bf1-309a-4486-91fb-18460f55c649)


To connect to your EC2 instance named "Docker-server" using MobaXterm, you can follow these steps:

1. **Open MobaXterm**: Launch MobaXterm on your local machine.

2. **Open SSH Session**:
   - Click on the "Session" button in the upper-left corner.
   - Select "SSH" as the session type.

3. **Configure SSH Session**:
   - In the "Remote host" field, enter the public IP address or the public DNS of your EC2 instance.
   - In the "Specify username" field, enter the username for your instance. For Amazon Linux 2, the default username is `ec2-user`.
   - In the "Advanced SSH settings" section, go to the "Use private key" field and select your .pem private key file that you downloaded when launching the instance.
   - Optionally, you can set a name for your session in the "Saved sessions" field to easily access it later.

4. **Connect**:
   - Click on the "OK" button to initiate the SSH connection.

5. **Authenticate**:
   - If prompted, confirm the connection and authenticate using the private key.

6. **Accessing the Instance**:
   - Once connected, you should have command-line access to your EC2 instance through MobaXterm.

Ensure that your EC2 instance is up and running and that your security group allows SSH traffic (port 22) from your IP address. Also, make sure you've set the appropriate permissions (`chmod 400`) on your .pem key file to ensure it's secure.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/14973698-bd2d-4035-8a03-aa69bfeddd40)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/1b546968-98cc-4293-84e6-356ae56c6e9e)


After connecting to your EC2 instance using SSH through MobaXterm, you can run the following commands to switch to the root user with sudo privileges and install Docker:

1. **Switch to root user with sudo**:
    ```bash
    sudo su -
    ```

   This command will prompt you for the password of the user you're connecting with. Enter the password and press Enter.

2. **Update the package index**:
    ```bash
    yum update
    ```

3. **Install Docker**:
    ```bash
    yum install docker
    ```

   This command installs Docker on your Amazon Linux 2 instance.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4110288d-bb31-4ef6-9543-2c8ad1ad62e3)

1. **Check Docker service status**:
    ```bash
    service docker status
    ```

   This command will show you the current status of the Docker service.

2. **Start Docker service**:
    ```bash
    service docker start 
    ```

   This command will start the Docker service.


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/7d4777de-9997-4d7e-b27f-56ff5154c696)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bdbd1623-55c5-4699-af7a-4968e9e757e7)

1. **Open your web browser**: Navigate to your preferred web browser.

2. **Go to Docker Hub**: Enter the URL https://hub.docker.com/ in the address bar and press Enter.

3. **Search for Tomcat image**: In the search bar at the top of the Docker Hub website, type "tomcat" and press Enter or click on the search icon.

4. **Browse Tomcat images**: Browse through the search results to find the Tomcat image that meets your requirements. There are typically multiple versions available, so choose the one that fits your needs.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/fcab069a-26cd-4796-8a4d-e6f9c757a3e2)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6da612d6-9b31-4b53-a680-135834d24246)

1. **Edit the hostname file**:
   Run the following command to edit the hostname file:
   ```bash
   sudo nano /etc/hostname
   ```
   
2. **Change the hostname**:
   Inside the text editor, modify the hostname to "dockerhost". It should only contain the single word "dockerhost".

3. **Save the changes**:
   After making the changes, press `Ctrl + O` to save the file, then press `Enter`. Press `Ctrl + X` to exit the editor.
   

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/54539055-6047-443a-8d96-9723151d5633)

If your system is using SysV init and you wish to reboot the system using `init 6`, you would typically execute it with superuser privileges:

```bash
init 6
```

This command will initiate the system shutdown and reboot.

To pull the official Tomcat Docker image from Docker Hub, you can use the following command:

```bash
docker pull tomcat
```

This command will pull the latest version of the Tomcat image by default. If you want to pull a specific version, you can specify it using a tag.



![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5bc6051a-4aba-488f-98a6-0da78484c24a)


To list all Docker images that are currently downloaded on your system, you can use the following command:

```bash
docker images
```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/839e5c9f-c704-42ee-874c-4ed469d6f914)

3. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/3d2510e7-0a52-43f4-ba81-e4abc0fdb28b)

Accessing

a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c7bd9fe6-ce70-42f9-82c5-a7244cf9aca3)

open 8081 port
b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/40f24703-e215-4891-9e44-3c2e3dbf319e)

c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/af370adb-a762-4ae1-9164-1fc256734899)

Fixing Tomcat Container Issue

1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a3b322b5-6a33-4b1f-a195-652ba1f10ba9)

2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/fc71abf0-03e3-4c43-931c-4792aa1b0052)

3. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/81ce55dc-5c2f-4948-8970-900facf67d1a)

4. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d8dd8452-022d-439e-b9ab-bcf8c10f0044)

   This changes done is Temporary so we creat docker file

   lets understand how can we do through dockerfile

   1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5143b378-e177-4f27-8608-20628aa00363)

   2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/17bd7f75-ba09-4c1c-99b5-0abab93da251)
  
   3. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/59e213a7-bbb4-44d2-be57-4a20b3926c46)
  
   4. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/e57a0500-c81b-476e-b7eb-c3661a3395c7)
  
   5. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/caac184b-5557-42fa-aa2d-8774c21933c5)
  
   integrate docker with jenkins

   a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/fce35dad-8ff1-42ee-9482-76e77cf3113e)

   b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5eeae8b1-a8a6-4dc7-ad69-150fe121c624)

   c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4a201549-eec3-47e7-b5f8-e7cf1df1833c)

   dockruser error

   1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/63cccc92-bd3b-4984-91a8-e4e2c49e5879)
  
   2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/02eeae5e-ee2b-4644-aa99-cc38c40e368e)

  
   3. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c70e5680-ab96-425d-83a1-c0ea2da9374f)
  
   4. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/27d300bc-c27d-4c95-88c4-3cce1786af04)
  
   5. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/85dd34a6-8d8d-4438-8103-4a13478e05c3)
  
   6. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/91ddb02d-e7b3-4076-bfe2-5364e1750bb7)


   Login to Jenkins

   a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/587774b6-69c6-48ef-998e-3779ee18a78f)

   Private ip

   b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/29a18eb9-ecb6-418b-b632-6fdee0708e64)

   c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/213eed6d-26c8-4bca-a25d-23c10d6318d0)

   d. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/1db80f52-03d6-4263-8cb3-01482a58b62b)











































