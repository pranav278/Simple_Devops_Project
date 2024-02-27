## Ansible Installation 
```
1. Setup EC2 instance
2. Setup Hostname
3. create anadmin user
4. Add user to sudoers file
5. Generate ssh keys
6. Enable password based login
7. install ansible

```




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


add this user to visudo

1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2e2c9342-71c6-47cb-a56c-0dd97b91deec)

2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/17fd2def-4865-47c3-9694-32a03f717e23)

3. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/7d851097-f4a9-43bc-9d04-bd6e488750dc)

4. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5ac8ccc8-b6e5-42b6-acea-f73033727a92)

Login to User Terminal

A. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/507b6387-a02e-4363-9234-eb9ef080e8ed)

b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/e542fc87-452e-4ddc-b4f0-945efc4f6b2d)

c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/60f93ee3-8193-4839-bec0-5e579edbbb06)

d. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bc52dbd8-9813-4044-884e-a6647232dd40)

integrate docker with ansible













