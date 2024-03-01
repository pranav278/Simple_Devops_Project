# Integrating Docker in CI/CD Pipeline

```

Step 1. Setup Docker Enviroment

```
Setup Docker Enviroment

## Step 1. Setup Docker Enviroment

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

---



---

## Step 2: Create a Tomcat Container

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

The `docker run` command you provided is used to start a new Docker container based on the Tomcat image, mapping port 8080 from the container to port 8081 on the host system. Here's a breakdown of the command:

```
docker run -d --name tomcat-container -p 8081:8080 tomcat
```


- `-d`: This flag runs the container in detached mode, meaning it runs in the background.
- `--name tomcat-container`: This flag assigns the name "tomcat-container" to the running container.
- `-p 8081:8080`: This flag maps port 8080 from the container to port 8081 on the host system. This means that you can access the Tomcat server running inside the container via port 8081 on the host system.
- `tomcat`: This is the name of the Docker image that you want to use to create the container. In this case, it's the official Tomcat image from Docker Hub

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/3d2510e7-0a52-43f4-ba81-e4abc0fdb28b)

Tomcat image, and you will be able to access the Tomcat server running inside the container by navigating to http://localhost:8081

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c7bd9fe6-ce70-42f9-82c5-a7244cf9aca3)

To allow traffic on port 8081, you need to ensure that the security group associated with your EC2 instance allows inbound traffic on that port.

Here are the steps to open port 8081 in the security group:

1. **Go to the EC2 Dashboard**: Navigate to the EC2 dashboard in the AWS Management Console.

2. **Select your Instance**: Click on the instance that you're running your Docker container on.

3. **Find Security Group**: Scroll down to the "Description" tab and find the "Security groups" section. Click on the linked security group name.

4. **Edit Inbound Rules**: In the Security Group dashboard, select the "Inbound rules" tab.

5. **Add Rule**: Click the "Edit inbound rules" button, then click "Add rule".

6. **Configure Rule**:
   - For "Type", select "Custom TCP Rule".
   - For "Port range", enter "8081".
   - For "Source", enter "0.0.0.0/0" to allow traffic from any IP address. Alternatively, you can specify a specific IP range if you want to restrict access.

7. **Save Changes**: Click the "Save rules" button to apply the changes.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/40f24703-e215-4891-9e44-3c2e3dbf319e)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/af370adb-a762-4ae1-9164-1fc256734899)

* lets Fix above Tomcat Container Issue

 Syntax for executing a bash shell inside a Docker container named `tomcat-container` would be:

```
docker exec -it tomcat-container /bin/bash
```


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a3b322b5-6a33-4b1f-a195-652ba1f10ba9)

Here is command to recursively copy all files and directories into the `webapps` directory would be:

```bash
cp -R * ../webapps/
```

This command copies all files and directories (except those whose names begin with a dot) from the current directory into the `webapps` directory located one level above the current directory. Make sure you're in the correct directory before executing this command to ensure that you copy the intended files and directories.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/fc71abf0-03e3-4c43-931c-4792aa1b0052)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/81ce55dc-5c2f-4948-8970-900facf67d1a)

* Now check our Tomcat server is up

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d8dd8452-022d-439e-b9ab-bcf8c10f0044)


* This changes done Temporary so we creat docker file

---




---

## Step 3: Create a Docker file

* lets understand how can we do through dockerfile

Dockerfile instruction:

```Dockerfile
FROM tomcat:latest

RUN cp -R /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps
```

This instruction will use the `tomcat:latest` base image, then it will run the `cp` command to recursively copy all files and directories from `/usr/local/tomcat/webapps.dist/` to `/usr/local/tomcat/webapps` within the container.

Make sure that the source directory `/usr/local/tomcat/webapps.dist/` contains the files you want to copy, and the destination directory `/usr/local/tomcat/webapps` exists within the container.


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5143b378-e177-4f27-8608-20628aa00363)

 
Build a Docker image with a specified tag would be:

```bash
docker build -t demotomcat .
```

This command tells Docker to build an image based on the Dockerfile in the current directory (`.`) and tag it with the name `demotomcat`. 
 
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/17bd7f75-ba09-4c1c-99b5-0abab93da251)
  
To list all Docker images currently available on your system, you can use the `docker images` command. Here's how you would use it:

```bash
docker images
```

Running this command will display a list of Docker images along with details such as the repository, tag, image ID, creation date, and size. This information can be helpful for managing your Docker images and containers.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/59e213a7-bbb4-44d2-be57-4a20b3926c46)

Running a Docker container with a specific name (`demotomcat-container`), mapping ports (`8085` on the host to `8080` in the container), and specifying the image (`demotomcat`) would be:

```bash
docker run --name demotomcat-container -p 8085:8080 demotomcat
```

This command will run a container from the `demotomcat` image, name it `demotomcat-container`, and map port `8085` on the host to port `8080` in the container.


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/e57a0500-c81b-476e-b7eb-c3661a3395c7)

* Lets, See out tomcat Server is up
  
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/caac184b-5557-42fa-aa2d-8774c21933c5)

---



---
  
## Step 4: Integrate docker with jenkins


To view the contents of the `/etc/group` file, you can use the `cat` command:

```bash
cat /etc/group
```

This command will display the contents of the `/etc/group` file on your system. The `/etc/group` file contains information about groups on the system, including group names, group IDs, and a list of users who are members of each group.

Verify Docker user is here or not
The `useradd` command is used to create a new user account on Unix-like operating systems. To create a new user named `dockeradmin`, you can use the following command:

```bash
sudo useradd dockeradmin
```

This command will create a new user account named `dockeradmin` on your system. By default, the `useradd` command creates a new user account with a home directory at `/home/dockeradmin`. However, you might want to specify additional options such as setting the home directory or assigning the user to specific groups depending on your requirements.

After creating the user account, you might also want to set a password for the new user using the `passwd` command:

```bash
sudo passwd dockeradmin
```

This command will prompt you to enter and confirm a password for the `dockeradmin` user. Once you've set the password, the user will be able to log in to the system.
  
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/fce35dad-8ff1-42ee-9482-76e77cf3113e)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5eeae8b1-a8a6-4dc7-ad69-150fe121c624)

Add the user `dockeradmin` to the `docker` group using the `usermod` command. However, the syntax you provided is incorrect. The correct syntax for adding a user to a group with `usermod` is:

```bash
sudo usermod -aG docker dockeradmin
```

In this command:

- `usermod` is the command to modify a user's account.
- `-aG` is an option specifying that you want to append (`-a`) the user to a group (`-G`).
- `docker` is the group you want to add the user to.
- `dockeradmin` is the user you want to add to the group.

After running this command, the user `dockeradmin` will be added to the `docker` group, allowing them to execute Docker commands without needing to use `sudo`. Remember that the changes will only take effect the next time the user logs in.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4a201549-eec3-47e7-b5f8-e7cf1df1833c)

* Try to login using Dockeruser but it will gets error 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/63cccc92-bd3b-4984-91a8-e4e2c49e5879)
  
To enable password authentication in the SSH server configuration file (`sshd_config`), you can use a text editor like `vi` to modify the file. Here's how you can do it:

```bash
sudo vi /etc/ssh/sshd_config
```

This command opens the `sshd_config` file in the `vi` text editor with superuser privileges.

Once you're in the `vi` editor, you need to find the line that controls password authentication. Look for a line that begins with `#PasswordAuthentication` (note the `#` at the beginning, which comments out the line). If you find this line, remove the `#` to uncomment it. If you don't find the line, you can add it.

Change or add the line to read:

```
PasswordAuthentication yes
```

This line enables password authentication for SSH.  
   
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/02eeae5e-ee2b-4644-aa99-cc38c40e368e)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c70e5680-ab96-425d-83a1-c0ea2da9374f)
  
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/27d300bc-c27d-4c95-88c4-3cce1786af04)
  
The command you provided, service sshd reload, is used to reload the SSH server configuration without disconnecting active SSH sessions  
   
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/85dd34a6-8d8d-4438-8103-4a13478e05c3)
  
* Now you can login as dockeradmin  

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/91ddb02d-e7b3-4076-bfe2-5364e1750bb7)


To add the "Publish over SSH" plugin to Jenkins, you typically follow these steps:

1. **Login to Jenkins**: Open your web browser and navigate to your Jenkins instance.

2. **Access Plugin Manager**: Once logged in, click on "Manage Jenkins" in the sidebar.

3. **Install Plugins**: Under "Manage Jenkins", click on "Manage Plugins". Here, you'll find a list of available plugins.

4. **Find "Publish over SSH" Plugin**: In the "Available" tab, use the search box to find the "Publish over SSH" plugin.

5. **Select Plugin**: Once you find the "Publish over SSH" plugin, check the checkbox next to it.

6. **Install**: Click on the "Install without restart" button. Jenkins will download and install the plugin.

7. **Restart Jenkins**: After the installation is complete, Jenkins will prompt you to restart. Click on the checkbox if you want to restart Jenkins immediately or choose to restart manually later.

8. **Configure Plugin**: After Jenkins restarts, go back to your Jenkins dashboard and navigate to the job where you want to use the "Publish over SSH" plugin. Configure the plugin according to your requirements.


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/587774b6-69c6-48ef-998e-3779ee18a78f)



To add a SSH server in Jenkins for connecting to your Docker host, you can follow these steps:

1. **Login to Jenkins**: Open your web browser and navigate to your Jenkins instance.

2. **Access Manage Jenkins**: Click on "Manage Jenkins" in the Jenkins dashboard.

3. **Navigate to SSH Servers**: Under "Manage Jenkins", select "Configure System".

4. **Add SSH Server**: Scroll down until you find the "SSH Servers" section. Click on the "Add" button to add a new SSH server configuration.

5. **Fill in SSH Server Details**:
   - Name: Enter a name for your SSH server, for example, "dockerhost".
   - Hostname: Enter the private IP address of your Docker host.
   - Username: Enter the username to use for SSH authentication, which in your case is likely "dockeradmin".
   - Check "Use password authentication".
   - Enter the password for the "dockeradmin" user in the provided field.

6. **Test Configuration**: After entering the details, you can click on the "Test Configuration" button to verify that Jenkins can successfully connect to the Docker host using SSH. This will confirm that your configuration is correct.

7. **Save Configuration**: Once you've verified that the configuration works, click on the "Save" or "Apply" button to save your changes.

After completing these steps, Jenkins should be configured to connect to your Docker host using SSH. You can use this SSH server configuration in your Jenkins jobs to perform tasks such as deploying Docker containers or executing commands on the Docker host.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/29a18eb9-ecb6-418b-b632-6fdee0708e64)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/213eed6d-26c8-4bca-a25d-23c10d6318d0)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/1db80f52-03d6-4263-8cb3-01482a58b62b)











































