# Integrate Ansible with Jenkins

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


### Build an Image and Create container on Ansible

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


b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d2a639e7-e7c2-4a48-b032-5ee4a9241d07)

c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a5d7fffb-c8fb-4956-8bc8-8087e45851a0)

1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/8c07c791-0574-48fe-a592-268a6a608ab5)

Now Check with Ansible Public ip 

a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/65ba00e5-786d-4d14-af74-18f846a5e276)

b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c6037bd9-98d7-4c92-b463-013e99a3bc85)













