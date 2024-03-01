# Integrating Ansible in CI/CD Pipeline 


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




 















