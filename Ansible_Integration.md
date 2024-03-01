# Integrating Ansible in CI/CD Pipeline 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/08dd370c-4b05-43b8-a176-de02e7fd25da)


```
Step 1: Ansible installation
Step 2: Integrate docker with ansible
Step 3: Integrate Ansible with Jenkins
Step 4: Build an Image and Create container on Ansible
Step 5: Ansible Playbook to Create image and Container
Step 6: Copy Imange on the dockerhub
Step 7: Jenkins Job to Build an Imange onto Ansible
Step 8: Create Container on Dockerhost using Ansibleplaybook
Step 9: Jenkins CI/CD to deploy on Contaner Using Ansible
```
---



---

## Step 1: Ansible installation


1. **Launch EC2 Instance**:
   - Go to the AWS Management Console and navigate to the EC2 dashboard.
   - Click on "Launch Instance" and choose the "Amazon Linux 2 AMI" as the image.
   - Select an instance type, configure instance details, add storage, and configure any additional settings as needed.
   - At the "Configure Security Group" step, create a new security group or use an existing one. Allow all traffic (All traffic, all protocols, all ports, source `0.0.0.0/0` ::/0) for simplicity, but it's recommended to restrict access based on your specific needs.
   - Review and launch the instance. When prompted, create a new key pair or use an existing one. Download the private key file (`.pem`).

2. **Connect using MobaXterm**:
   - Open MobaXterm.
   - Go to "Session" and click on "SSH".
   - In the "Remote host" field, enter the public IP address or DNS of your EC2 instance.
   - In the "Advanced SSH settings" section, click on the "Use private key" checkbox and browse to select the private key file (`.pem`) you downloaded during instance creation.
   - Click "OK" to connect.

3. **Configure SSH Key Permissions**:
   - Before connecting, ensure that the permissions on your private key file are secure. In Unix/Linux systems, you typically do this with the `chmod` command:
     ```
     chmod 400 /path/to/your/private-key.pem
     ```

4. **Connect to the Instance**:
   - Once you've configured the session in MobaXterm, double-click on it to initiate the SSH connection to your EC2 instance.
   - If everything is set up correctly, you should be connected to your EC2 instance via SSH.

5. **Further Configuration**:
   - Once connected, you can proceed with any further configurations you need on your EC2 instance, such as installing Ansible, setting up your playbooks, etc.

That's it! You should now have your EC2 instance set up with the specified configuration and connected to it using MobaXterm.




![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a7e3b4c6-f242-4a16-95c8-3c67d082d418)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6b857048-68d3-45bc-a0af-f31290ce3a67)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/e5058350-4280-4505-b0ef-2c30c13d616d)

To change the hostname of your EC2 instance to "ansible-server", you can follow these steps after connecting to the instance via SSH:

1. **Edit the Hostname File**:
   - Use a text editor like `vi` or `nano` to edit the `/etc/hostname` file:
     ```
     sudo nano /etc/hostname
     ```

2. **Change the Hostname**:
   - Replace the existing hostname with the new hostname "ansible-server".
  

3. **Restart the Server**:
   - Simply execute the following command to initiate a system restart:
     ```
      init 6
     ```

 To give `sudo` privileges to a user, create a new user named `ansadmin`, and generate a password for it, follow these steps:

1. **Switch to Root User**:
   - If you're not already the root user, switch to root using:
     ```
     sudo su -
     ```

2. **Create the User**:
   - Use the `adduser` command to create the `ansadmin` user:
     ```
     adduser ansadmin
     ```

3. **Set Password for the User**:
   - After creating the user, set a password for the `ansadmin` user:
     ```
     passwd ansadmin
     ```
   You will be prompted to enter and confirm the password for the user.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/abf98d3b-e9fa-41bf-987b-87b3765793e5)


To add the `ansadmin` user to the `sudoers` file using `visudo`, which is the recommended way to edit the sudoers file, follow these steps:

1. **Open sudoers File for Editing**:
   - As root, open the sudoers file using `visudo`:
     ```
     sudo visudo
     ```

2. **Navigate to the sudoers Configuration**:
   - Use the arrow keys to navigate to the appropriate section in the sudoers file.

3. **Add User to sudoers**:
   - Add the following line to grant `sudo` privileges to the `ansadmin` user:
     ```
     ansadmin ALL=(ALL) ALL
     ```

   This line allows the user `ansadmin` to run any command as any user using `sudo`.

4. **Save and Exit**:
   - After making the necessary changes, save and exit the editor. In `vi` (the default editor for `visudo`), you can do this by pressing `Esc` to exit editing mode, then typing `:wq` to save and quit.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2e2c9342-71c6-47cb-a56c-0dd97b91deec)


To enable password authentication in the `sshd_config` file, follow these steps:

1. **Open `sshd_config` for Editing**:
   - You can use a text editor like `nano` or `vi` to open the `sshd_config` file. Here's how to do it with `nano`:
     ```
     sudo nano /etc/ssh/sshd_config
     ```

2. **Find the Password Authentication Setting**:
   - In the `sshd_config` file, look for the line that begins with `PasswordAuthentication`. By default, it is usually set to `no`.
   - If you can't find the line, you can add it manually.

3. **Modify the Password Authentication Setting**:
   - Change `PasswordAuthentication no` to `PasswordAuthentication yes`.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/17fd2def-4865-47c3-9694-32a03f717e23)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/7d851097-f4a9-43bc-9d04-bd6e488750dc)


If you're using a system with SysVinit, the command `service sshd reload` would reload the SSH service configuration without interrupting existing SSH sessions. 

```bash
service sshd reload
```

This command will reload the SSH service configuration without terminating active SSH sessions. Any changes made to the SSH server configuration files, such as `sshd_config`, will take effect after running this command.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5ac8ccc8-b6e5-42b6-acea-f73033727a92)

Now login to the terminal as the ansadmin user

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/507b6387-a02e-4363-9234-eb9ef080e8ed)

1. Once logged in, you can generate an SSH key pair by running the `ssh-keygen` command:

```bash
ssh-keygen
```

3. You will be prompted to specify the location to save the key pair. Press Enter to save the keys in the default location (`/home/ansadmin/.ssh/id_rsa`).

4. You can optionally enter a passphrase for added security, or leave it empty for no passphrase. Press Enter to continue.

5. The `ssh-keygen` command will generate a public/private key pair and display a message confirming the generation of the keys.

6. Your public key will be stored in `/home/ansadmin/.ssh/id_rsa.pub`, and your private key will be stored in `/home/ansadmin/.ssh/id_rsa`.

7. You can now use this SSH key pair to authenticate with other servers or services.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/e542fc87-452e-4ddc-b4f0-945efc4f6b2d)


1. **Install Ansible**:
   Amazon Linux 2 offers Ansible as an extra package, which can be installed using `amazon-linux-extras`:
   ```bash
   sudo amazon-linux-extras install ansible2
   ```

   This command installs Ansible version 2.x on your system.

2. **Verify Installation**:
   After installation, you can verify the Ansible version to ensure it was installed correctly:
   ```bash
   ansible --version
   ```

   This command will display the installed version of Ansible.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/60f93ee3-8193-4839-bec0-5e579edbbb06)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bc52dbd8-9813-4044-884e-a6647232dd40)

---



---

## Step 2: Integrate docker with ansible

* Manage Dockerhost with Ansible

```
On Docker Server
- Create ansadmin
- Add ansadmin to sudoers files
- nable Password based login

On Ansible Node
- Add hosts file
- Copy ssh keys
```

* Login to Docer server :-

1. **Go inside root by sudo su -**:
   After logging in, switch to the root user using the `sudo su -` command:

   ```bash
   sudo su -
   ```

   This command will prompt you for the root user's password. Enter the password to switch to the root user.

2. **Create Ansible User ansadmin with Password**:
   Once you're logged in as the root user, you can create a new user named `ansadmin` with a password. Use the `useradd` and `passwd` commands to achieve this:

   ```bash
   useradd -m ansadmin  # Create the user with home directory
   passwd ansadmin      # Set a password for the user
   ```

   You will be prompted to enter and confirm the password for the `ansadmin` user.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/506e29e5-660a-43bf-9fff-9b556402418d)

To add the `ansadmin` user to the sudoers list and grant it sudo privileges, you should edit the sudoers file using the `visudo` command. Here's how you can do it:

1. As root, run the `visudo` command to open the sudoers file for editing:
   ```bash
   visudo
   ```

2. Add a new line to grant sudo privileges to the `ansadmin` user. The line should look like this:
   ```
   ansadmin    ALL=(ALL)       ALL
   ```

   This line allows the `ansadmin` user to run any command with sudo privileges.




![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/accad171-3ce1-47d1-baa1-22502086313e)

To check if password authentication is enabled for SSH on your server, you can inspect the SSH daemon configuration file (`sshd_config`). Here's how you can do it:


1. Open the SSH daemon configuration file (`sshd_config`) using a text editor. Typically, this file is located at `/etc/ssh/sshd_config`:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

2. Look for the line that starts with `PasswordAuthentication`. This line determines whether password authentication is enabled. It should look like this:
   ```
   PasswordAuthentication yes
   ```

3. If the value is set to `yes`, it means password authentication is enabled. If it's set to `no`, password authentication is disabled.

4. Make any necessary changes to the `PasswordAuthentication` line. If you had to make changes, save the file and exit the text editor.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/980041e8-b678-4d6b-833a-6e0f021b55d9)


* Login to Ansible Server :-

Add Docker Server as a managed node in ansible inventory

Get ip of docker server

Here's how you can use `ifconfig` to view network interface information:

```bash
ifconfig
```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d43ba79d-6ea7-409f-857d-6776532cdd49)

To add the public IP address of a Docker server to your Ansible inventory, follow these steps:

1. Open the Ansible hosts file using a text editor. You can use `sudo` to edit it with elevated privileges:

```bash
sudo nano /etc/ansible/hosts
```

After adding the Docker server to your Ansible inventory, you can manage it like any other host using Ansible commands and playbooks. 

To add an IP address to the Ansible inventory file located at `/etc/ansible/hosts` using the `vi` text editor, you would follow these steps:

1. Open the file in `vi` for editing:
   ```bash
   sudo vi /etc/ansible/hosts
   ```
2. Press `i` to enter insert mode. This allows you to add content to the file.
3. Add the IP address in the format `<IP_address>` followed by any additional configuration, such as specifying a group or assigning variables.
4. Once you've added the IP address or addresses, press `Esc` to exit insert mode.
5. Save the changes and exit `vi`:
   - Type `:wq` and press `Enter` to save and quit.
   - Alternatively, type `:x` and press `Enter` to save and quit.

Here's an example of how your `/etc/ansible/hosts` file might look after adding an IP address:

```plaintext
Docker Ip
192.168.1.100
```



![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/7a0acf43-518c-4dda-9e03-515790425e66)


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/8d2593da-1cf8-419e-aeba-5d83cfdfac01)

* We need to keep secure this keys

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d9e4a05b-f457-4f97-9fad-7e7f1180b611)

The `ssh-copy-id` command is used to securely copy a user's public key to a remote server's `authorized_keys` file, allowing the user to authenticate to the remote server using public key authentication.

To use `ssh-copy-id` to copy your public key to the server with IP address `172.31.39.87`, you would typically run the following command:

```bash
ssh-copy-id 172.31.39.87
```
 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0b22433a-9ebd-4e1e-9c53-2cb09dd600ed)

* Highlighted ip is the ip of Docker server

* Keys Pairs are copied to remote server ( authorised keys )

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/92e77f22-66de-4555-89bb-4d33638be4bb)

* Now check you Able to connect to systems or not
* To use Ansible to ping all hosts in your inventory, you can run the following command:

```bash
ansible all -m ping
```

This command instructs Ansible to use the `ping` module (`-m ping`) against all hosts (`all`) in your inventory.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/cccb18a8-12f3-4b7a-ab39-a32ee92209d5)


* Now Ansible able to connect with our docker without any Credentials

---




---

## Step 3: Integrate Ansible with Jenkins

* Go to Jenkins 

1. **Configure SSH Credentials**:
   - Go to "Manage Jenkins" > "Manage Credentials" > "System" > "Global credentials (unrestricted)" > "Add Credentials".
   - Choose "SSH Username with private key" as the kind of credentials.
   - Fill in the necessary information:
     - Username: `ansadmin`
     - Private Key: Select "Enter directly" and paste the private key associated with the `ansadmin` user.
     - ID: Give it a unique ID, e.g., `ansible-ssh-key`.
     - Description: Provide a meaningful description.
   - Click "OK" to save the credentials.


2. **Configure SSH Server**:
   - Go to "Manage Jenkins" > "Configure System".
   - Scroll down to the "SSH Servers" section.
   - Click on "Add SSH Server" and provide the following information:
     - Name: `ansible-server`
     - Hostname: Private IP address of your Ansible server
     - Credentials: Select the SSH username and private key you added in the previous step (`ansadmin` and the associated private key).
   - Click "Save" to save the configuration.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a1ccf21c-161f-4842-b1da-4c27f3ca21ec)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/8caeb4fc-1145-4ea6-ac61-c4d8f891461d)


lets, Create New Job ( CopyArtifacts_onto_Ansible )

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/01f3f125-397c-4801-884f-7bde3379feec)

Remove the Poll SCM

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/69aee5c2-327c-40d6-9a9d-6bcd41e8f87d)

Add this Configuration 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/848870d4-0680-4193-ac53-1396e059a4b3)

To create a remote directory named "docker" and change its permissions using the command line, you would typically use SSH to connect to the remote server and then execute the necessary commands. Here's how you can do it:

1. **Create Remote Directory**:
   
   ```
   mkdir docker
   ```

   Replace `username` with your actual username and `remote_host` with the hostname or IP address of the remote server.

2. **Change Permissions**:

   ```
   sudo chown ansadmin:ansadmin docker
   ```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/dee8df72-b48f-4bc1-bc20-1c8a13a38c79)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/1b88832c-a32d-4457-a09e-0e8fac51a422)

To implement the requested changes in the Jenkins job configuration, you need to navigate to the Jenkins dashboard, locate the job you want to modify, and then follow these steps:

1. **Configure the Transfer Set**:
    - Go to the job's configuration page.
    - Find the section related to file transfer or publishing artifacts. This might be under the "Post-build Actions" section or similar, depending on your job configuration.
    - Look for an option related to transferring files or publishing artifacts. It might be named something like "Send files or execute commands over SSH" or "Publish over SSH".
    - Click on the option to configure it.

2. **Define Source Files**:
    - In the configuration for the file transfer, look for a field where you can specify the source files.
    - Set the source files to `webapp/target/war`.

3. **Remove Prefix**:
    - Look for an option or field where you can specify a prefix to remove.
    - Enter `webapp/target` in this field.

4. **Set Remote Directory**:
    - Find the field where you can specify the remote directory.
    - Set the remote directory to `//opt//docker`.

5. **Save Changes**:
    - Once you have made these modifications, ensure to save the changes to the Jenkins job configuration.



![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2cde069e-7ac6-4007-9e7d-df17d2d369df)


* lets, Save and Apply Build

* See the build is Succeeded 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/96ef1cd2-6ffa-47f9-a48c-ad3049237c62)

* war file is under docker repository 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/80a61987-f20c-4c27-a9d5-4f4d4d2975c7)

---




---

## Step 4: Build an Image and Create container on Ansible

Install Docker on Ansible-server as a user


```bash
sudo yum install docker -y
```

This command will install Docker on your system with the necessary dependencies without requiring manual confirmation during the installation process. Make sure you have sudo privileges to execute this command.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6474a8a5-86bd-4d54-b909-c9261636c3ac)


To add a user to the Docker group on Linux, you can use the `usermod` command. Here's the general syntax:

```bash
sudo usermod -aG docker username
```

Replace `username` with the name of the user you want to add to the Docker group. Here's a breakdown of the command:

- `sudo`: This command is used to execute subsequent commands with superuser privileges.
- `usermod`: This command is used to modify a user account.
- `-aG`: This option is used to add a user to a supplementary group.
- `docker`: This is the name of the group you want to add the user to.
 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2929ba5a-7479-432a-bf61-5343ffbc423e)

To check the group memberships of a user, you can use the `id` command followed by the username. Here's the command:

```bash
id username
```
To start the Docker service on a Linux system using the `service` command, you would typically use the following syntax:

```bash
sudo service docker start
```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/36b2ce82-d996-44df-a690-46e2dd444eee)

Create Dockerfile on Ansible Server
To edit or create a Dockerfile using the `vi` text editor, you would typically run the following command:

```bash
vi Dockerfile
```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/7a599455-3f83-4e73-b150-6d707d1f2c99)

Here's how you can write this into your Dockerfile:

```Dockerfile
# Use the official Tomcat image as the base
FROM tomcat:latest

# Copy contents of webapps.dist into webapps directory
RUN cp -R /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps

# Copy your .war files into the webapps directory
COPY *.war /usr/local/tomcat/webapps/
```

Let me explain the commands:

- `FROM tomcat:latest`: This sets the base image as the official Tomcat image.
  
- `RUN cp -R /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps`: This command copies all the contents from the `webapps.dist` directory in the Tomcat image to the `webapps` directory. The `-R` flag is used for recursively copying subdirectories and files.

- `COPY *.war /usr/local/tomcat/webapps/`: This command copies all `.war` files from the current directory (where your Dockerfile is located) into the `webapps` directory in the Tomcat image.

Make sure your `.war` files are in the same directory as your Dockerfile when you build the Docker image.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d2a639e7-e7c2-4a48-b032-5ee4a9241d07)

To build the Docker image with the provided Dockerfile, you can run the following command:

```bash
docker build -t regapp:v1 .
```

Let's break down the command:

- `docker build`: This command is used to build a Docker image.
- `-t regapp:v1`: This flag tags the built image with the name `regapp` and the tag `v1`.
- `.`: This specifies the build context. In this case, the Dockerfile is assumed to be in the current directory, and `docker build` will look for it there.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a5d7fffb-c8fb-4956-8bc8-8087e45851a0)

Run a Docker container based on the `regapp:v1` image, intending to map port 8080 from the container to port 8081 on your host machine. 

```bash
docker run -t --name regapp-server -p 8081:8080 regapp:v1
```

Let's break down the command:

- `docker run`: This command is used to create and start a Docker container.
- `-t`: This flag allocates a pseudo-TTY, which is generally used to keep STDIN open.
- `--name regapp-server`: This flag assigns a name to the container as `regapp-server`.
- `-p 8081:8080`: This flag maps port 8080 from the container to port 8081 on the host machine.
- `regapp:v1`: This is the name and tag of the Docker image you want to use to create the container.


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/8c07c791-0574-48fe-a592-268a6a608ab5)

* Now Check with Ansible Public ip tomcat server is up 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/65ba00e5-786d-4d14-af74-18f846a5e276)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c6037bd9-98d7-4c92-b463-013e99a3bc85)

---



---

## Step 5: Ansible Playbook to Create image and Container 


First Login to Ansible-Server as ansadmin

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/8edc6442-a348-44e1-9804-096b806e2875)


To copy the public IP address of the Ansible server using the `ifconfig` command and then paste it into the Ansible inventory file, you can follow these steps:

1. Use the `ifconfig` command to find the public IP address. If the Ansible server is connected to the internet directly, you can find the public IP under the network interface that connects to the internet (usually named something like `eth0` or `ens3`).

Here's how you can find the public IP address using `ifconfig`:

```bash
ifconfig
```

Look for the interface connected to the internet (it's usually marked as "inet" or "inet addr"), and note down the associated IP address. It should look something like `x.x.x.x`.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/fe19c2a3-266a-4833-b34c-7ab1551ae870)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/90560310-d017-4e86-b8de-e8b914197c4a)

In summary, the effect of editing the Ansible inventory file to include the public IP of the Ansible server ensures that Ansible can target and manage the server effectively during playbook runs or any other Ansible operations.


The command you would run to display the uptime for all hosts using Ansible is:

```bash
ansible all -a "uptime"
```
Ansible Inventory: Ansible will look at the inventory file specified by default (/etc/ansible/hosts or any other specified inventory file) to determine which hosts to connect to. If you have hosts listed under the [all] group or another group specified after ansible, it will target those hosts.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/ad071d5e-e173-4ab2-b403-d812466d12c8)

It seems like you're experiencing an issue where Ansible is able to connect to Docker hosts but not to the Ansible server itself. This could indeed be due to SSH keys not being copied to the Ansible server.


Running `ssh-copy-id localhost` will copy your SSH public key to the `~/.ssh/authorized_keys` file on the localhost itself. This allows you to SSH into the localhost without needing to enter a password, assuming SSH key authentication is enabled.

Here's how you can run it:

```bash
ssh-copy-id localhost
```

After running this command, you'll be prompted to enter the password for your user account on the localhost. Once you enter the password, your SSH public key will be appended to the `authorized_keys` file in the `~/.ssh` directory of your localhost's user account.

From that point onward, you'll be able to SSH into localhost without being prompted for a password, as long as your SSH configuration allows key-based authentication.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5807122c-d524-4231-a8f2-dd9eaa30b76e)


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a32b3867-3c6b-4d8a-9edd-51e5df5af8ae)

Now it showing for both because we copied both the keys


### lets Create the simple Ansible Playbook

```yaml
---
- hosts: ansible
  tasks:
    - name: Create Docker Image
      command: docker build -t regapp:latest .
      args:
        chdir: /opt/docker
```

Explanation:

- `hosts: ansible`: This specifies that the tasks in this playbook should be executed on hosts listed under the `ansible` group in your Ansible inventory file.
  
- `tasks`: This is where you define the tasks to be executed.

- `- name: Create Docker Image`: This is a task name for better readability and identification.

- `command`: This specifies the shell command to be executed, which in this case is `docker build -t regapp:latest .`, where:
  - `docker build` is the Docker command to build an image.
  - `-t regapp:latest` tags the image with the name `regapp` and the tag `latest`.
  - `.` indicates that the Dockerfile is located in the current directory.

- `args`: This is used to provide additional arguments to the command.
  
- `chdir: /opt/docker`: This sets the working directory to `/opt/docker`, meaning that the `docker build` command will be executed in this directory where the Dockerfile is located.

Make sure your inventory file has the `ansible` group defined and that the hosts you want to target are listed under this group. Additionally, ensure that your Ansible control node has SSH connectivity to these hosts and that Docker is installed and running on them.


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5b024e08-9666-4a24-8170-41016fb07933)

Running `ansible-playbook regapp.yml --check` with the `--check` flag means Ansible will perform a "dry run". It will simulate the execution of the playbook without actually making any changes on the target hosts. Instead, it will report what changes would have been made.

Here's how you would run it:

```bash
ansible-playbook regapp.yml --check
```

This is useful for verifying what actions Ansible would take without making any actual changes. It's a good practice to use `--check` before applying changes, especially in production environments, to avoid unintended consequences.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a0b10298-44f5-46ec-b6a8-779d893a996e)

---



---

## Step 6: Copy Imange on the dockerhub

To create a Docker Hub account, follow these steps:

1. **Go to Docker Hub Website**: Open your web browser and navigate to the Docker Hub website: [https://hub.docker.com/](https://hub.docker.com/).

2. **Sign Up**: Click on the "Sign Up" button located at the top right corner of the page.

3. **Fill Out the Form**: Fill out the sign-up form with the required information, including:
   - Username: Choose a unique username for your Docker Hub account.
   - Email Address: Provide your email address.
   - Password: Choose a strong password for your account.

4. **Agree to Terms of Service and Privacy Policy**: Check the box to agree to Docker's terms of service and privacy policy.

5. **Complete Sign Up**: Click on the "Sign Up" button to complete the registration process.

6. **Verify Email (if required)**: Depending on Docker Hub's current policies, you may need to verify your email address by clicking on a link sent to the email you provided during sign-up.

7. **Set Up Docker Hub Account**: Once your account is created and verified (if required), you can log in to Docker Hub using your username and password.

To log in to Docker Hub from the command line using the Docker CLI, follow these steps:

1. Open your terminal or command prompt.

2. Run the following command:

```bash
docker login
```

3. You'll be prompted to enter your Docker Hub username and password.

   ```plaintext
   Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
   Username: your_dockerhub_username
   Password: your_dockerhub_password
   ```

   Replace `your_dockerhub_username` with your Docker Hub username and `your_dockerhub_password` with your Docker Hub password.

4. After entering your credentials, press Enter. If the login is successful, you'll see a message indicating that you are logged in.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/21d1aec4-cb34-4df5-bb16-d2a54138eed1)


* We cannot direclty Push to Dockerpush because it could not Reconize account, it throws Below error

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/55ea2d1e-7676-41b1-bf32-bb6fe89ce90e)

To tag a Docker image, you can use the `docker tag` command followed by the image ID and the desired tag. Here's how you can tag the Docker image:

```bash
docker tag 80b9d41a2669 pranav280499/regapp:latest
```

Explanation:
- `80b9d41a2669` is the image ID of the Docker image you want to tag.
- `pranav280499/regapp:latest` is the new tag you want to assign to the image. This format follows the pattern `[username]/[repository]:[tag]`.

After running this command, the Docker image with the ID `80b9d41a2669` will be tagged with the name `pranav280499/regapp` and the tag `latest`. This allows you to reference the image more conveniently using the new tag.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/58d975ac-184f-44c6-a010-c3aefef911eb)

To push a Docker image to Docker Hub or any other Docker registry, you can use the `docker push` command followed by the image name and tag. Here's how you can push the image `pranav280499/regapp:latest` to Docker Hub:

```bash
docker push pranav280499/regapp:latest
```

Explanation:
- `pranav280499/regapp:latest` is the name of the Docker image along with the tag `latest` that you want to push to Docker Hub. This format follows the pattern `[username]/[repository]:[tag]`.

After running this command, Docker will push the specified image to Docker Hub under your Docker Hub account. Make sure you're logged in to Docker Hub (`docker login`) with appropriate permissions to push images to the repository `pranav280499/regapp`.

Ensure that your Docker image is properly tagged and built before pushing it to the Docker registry.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c2272f14-9ebf-4e3f-bbc1-dd3bea3926ea)

* See the dockerhub repository, our image will shows

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d5ec559f-b7f3-4652-93b3-fc1798f0646d)

---




---

## Step 7: Jenkins Job to Build an Imange onto Ansible

Modify Changes in our yml file
```
---
- hosts: ansible

  tasks:
  - name: Create Docker Image
    command: docker build -t regapp:latest .
    args:
     chdir: /opt/docker

  - name: Creat tag to push image onto dockerhub
    command: docker tag regapp:latest pranav280499/regapp:latest

  - name: push docker image
    command: docker push pranav280499/regapp:latest

```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0d34331b-34fb-4029-8b82-963693ad6ed2)

Explanation:

1. **Create Docker Image**:
   - This task builds a Docker image with the tag `regapp:latest` from the Dockerfile located in the `/opt/docker` directory.

2. **Create Tag to Push Image onto Docker Hub**:
   - This task tags the locally built image `regapp:latest` with the tag `pranav280499/regapp:latest`. This step is necessary to prepare the image for pushing it to Docker Hub.

3. **Push Docker Image**:
   - This task pushes the tagged Docker image `pranav280499/regapp:latest` to Docker Hub. This makes the image available in your Docker Hub repository.

Now check the file


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c0b173dd-c0e9-489c-aaef-f3a795856dd5)

To run the `regapp.yml` playbook with a limit to execute tasks only on the host with the IP address `172.31.46.162`, you can use the `--limit` option with `ansible-playbook`. Here's the command:

```bash
ansible-playbook regapp.yml --limit 172.31.46.162
```

Explanation:
- `ansible-playbook`: Command to execute an Ansible playbook.
- `regapp.yml`: Name of the playbook file.
- `--limit 172.31.46.162`: Limits execution to the host with the specified IP address.

This command will run the tasks defined in the `regapp.yml` playbook, but it will only execute them on the host with the IP address `172.31.46.162`. This is useful when you want to target specific hosts in your inventory for playbook execution. Make sure that the inventory file (`/etc/ansible/hosts` by default) contains an entry for the host with the specified IP address.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/3070a439-d610-4ca0-9b74-05e2dd6ca5ff)

To configure Jenkins to run an Ansible playbook after copying artifacts onto the Ansible server, follow these steps:

1. **Go to Jenkins Dashboard**: Log in to Jenkins and navigate to the Jenkins dashboard.

2. **Edit CopyArtifacts_onto_Ansible Job**:
   - Find and click on the "CopyArtifacts_onto_Ansible" job to edit its configuration.

3. **Add Post-Build Step**:
   - Scroll down to the "Post-build Actions" section.
   - Click on "Add post-build step"
4. **Enter Exec Command**:
   - In the command field, enter the following command to run the Ansible playbook:
     ```bash
     ansible-playbook /opt/docker/regapp.yml 
     ```
     Replace `/opt/docker/regapp.yml` with the path to your Ansible playbook.
     

5. **Enable SCM**:
   - If your Jenkins job is configured to use source code management (SCM), enable it and configure it according to your requirements.

6. **Schedule Job**:
   - Set the schedule for the job by specifying the cron expression in the "Build Triggers" section. Use `* * * * *` to trigger the job every minute.

7. **Apply and Save**:
   - Click on "Apply" and then "Save" to apply the changes to the Jenkins job configuration.



![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/624a0674-9467-4757-8c74-cd583fcd6d18)


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/ba4ca1be-b7e5-4172-a59d-0c52e254efb1)


### Lets Make Changes in index.jsp file through GIT and see our job status

Go to the index.jsp file and make Some Change and Push to origin master

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2e62042d-89fc-4c09-94a6-e96b2fd853aa)

Now see our build is triggered and and Finished Sucess 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4f17365b-7ae0-41dd-8cec-5c4b244a7cf8)

See here, webapp.war file generated with latest timestamp 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/be80efd1-1953-4a6a-a62b-ead553fbdbff)

Also new imange pushed to dockerhub 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/9f175a4a-053c-49ae-8f6d-e3af07cc73d3)

---



---

## Step 8: Create Container on Dockerhost using Ansibleplaybook
```
---
- hosts: dockerhost

  tasks:
  - name: create container
    command: docker run -d --name regapp-server -p 8082:8080 pranav280499/regapp:latest
```


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f32578eb-e405-4558-b51e-1901e91dd3af)

Explanation:

- `hosts: dockerhost`: Specifies that the tasks in this playbook should be executed on hosts listed under the `dockerhost` group in your Ansible inventory file.

- `tasks`: This is where you define the tasks to be executed.

- `- name: Create Container`: A description for the task for better identification.

- `command`: Specifies the shell command to be executed, which in this case is `docker run -d --name regapp-server -p 8082:8080 pranav280499/regapp:latest`, where:
  - `docker run` is the command to run a Docker container.
  - `-d` runs the container in detached mode (background).
  - `--name regapp-server` sets the name of the container to `regapp-server`.
  - `-p 8082:8080` maps port 8080 of the Docker container to port 8082 of the Docker host.
  - `pranav280499/regapp:latest` is the Docker image to use for creating the container.

This playbook will create a Docker container named `regapp-server` from the `pranav280499/regapp:latest` image and expose port 8080 of the container to port 8082 on the Docker host. Make sure that the `dockerhost` group is properly defined in your Ansible inventory file, and the Docker daemon is running on the target host.


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d52dd5e0-83ab-4d49-b234-5ff6a571b043)

Now check the yml file 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/12b8b7f2-00f3-43dc-8c79-690c51338875)

* Now login to Dockerhost Delete all the images and Container of Dockerhost

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/60a11b68-cb0d-426e-a486-d9c9ceebd801)


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/35a5d61a-7b61-4f66-a6dd-8aed534e0d16)


Now lets try to pull image from dockerhub as a ansadmin using ansibleplaybook

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/1e8ab9ec-7481-4823-ae74-dc7100279aec)

* Its Giving Error Due to Permission

Give the Permission to error path by chmod

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/543c37ff-5efe-4f30-8423-f96fa7a3ba6f)

Now see its Executing Successfully,.Hope image and Container Gets Created 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5f006298-fda8-4ba9-ade6-44c6dc89af9a)

Now check image and Container Created or not into docker host

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/16dc25b1-8df2-4888-b4e1-7646b3f9d3d0)

So, Out Container is running up lets see our server page

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2643a7e3-ffc9-42db-80c5-fc4816def8a4)


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/eae8b0a0-d754-44aa-a3ca-b9517f3d7a69)

* !! Successfully Running !!


### If We run playbooks once again, Container alredy Present lets see how to Resolve this issue


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0468a1c3-e972-4cef-9b5b-71a2834bd211)

Above error indicates that Container is already Present so lets modify our yml file
```
---
- hosts: dockerhost

  tasks:
  - name: stop existing Container
    command: docker stop regapp-server

  - name: remove the container
    command: docker rm regapp-server

  - name: remove imange
    command: docker rmi  pranav280499/regapp:latest
  - name: create container
    command: docker run -d --name regapp-server -p 8082:8080 pranav280499/regapp:latest

 
```


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5914b9ba-6f92-4ff4-b97b-8bc8cda16270)

* There is no Containor So we will Get this belowError


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/3b48fb1a-2e2f-42db-b9cd-4e9dafb66c70)

So, Modify File as

```
---
- hosts: dockerhost

  tasks:
  - name: stop existing Container
    command: docker stop regapp-server
    ignore_errors: yes

  - name: remove the container
    command: docker rm regapp-server
    ignore_errors: yes

  - name: remove image
    command: docker rmi pranav280499/regapp:latest
    ignore_errors: yes

  - name: create container
    command: docker run -d --name regapp-server -p 8082:8080 pranav280499/regapp:latest



```
Explanation:

- `hosts: dockerhost`: Specifies that the tasks in this playbook should be executed on hosts listed under the `dockerhost` group in your Ansible inventory file.

- `tasks`: This is where you define the tasks to be executed.

- `- name: Stop existing Container`: A description for the task for better identification. The `docker stop` command is used to stop the Docker container named `regapp-server`. The `ignore_errors: yes` parameter is used to ignore errors if the container is not running.

- `- name: Remove the container`: This task removes the Docker container named `regapp-server`. The `ignore_errors: yes` parameter is used to ignore errors if the container doesn't exist.

- `- name: Remove image`: This task removes the Docker image `pranav280499/regapp:latest`. The `ignore_errors: yes` parameter is used to ignore errors if the image doesn't exist.

- `- name: Create container`: This task creates a new Docker container named `regapp-server` from the image `pranav280499/regapp:latest` and exposes port 8080 of the container to port 8082 on the Docker host.

Ensure that the `dockerhost` group is properly defined in your Ansible inventory file, and the Docker daemon is running on the target host. Additionally, ensure that you have appropriate permissions to execute Docker commands on the target host.



![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/80ffef22-0143-4d8a-a878-361a6bfa8d3a)

Now lets run and Check

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d889bcef-cf63-49b7-ae96-471d91eade80)

Check Container and Images are created or not

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/637c3def-c71e-405c-97c3-72e015b62ad4)


So Now its Created, Lets automate with Jenkins

---




---

## Step 9: Jenkins CI/CD to deploy on Contaner Using Ansible

1. Make the Chnages in Exec Command add our deply.yml file including path

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/ae7cf16b-b390-44f7-86f1-d3b9f66034a9)


* Lets make change in index.jsp file


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a1a0ea02-8fc7-4d2e-9c6e-91fc71838e87)


* Lets Build it and See


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/601a4f20-f210-46bb-ae6d-d954787041ba)

* Container and images created Successfully.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/b1fd7199-273e-4061-b5f1-c0911a9ebe1b)

* Lets Check on Our Browser 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/537a37c9-acca-4a17-ad24-2294afc1b92c)

---

---


 















