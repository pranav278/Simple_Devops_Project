# Ansible Playbook to Create image and Container 



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

### Copy Imange on the dockerhub

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

### Jenkins Job to Build an Imange onto Ansible

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


### Create Container on Dockerhost using Ansibleplaybook
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
Explanation:

- `hosts: dockerhost`: Specifies that the tasks in this playbook should be executed on hosts listed under the `dockerhost` group in your Ansible inventory file.

- `tasks`: This is where you define the tasks to be executed.

- `- name: Stop existing Container`: A description for the task for better identification. The `docker stop` command is used to stop the Docker container named `regapp-server`. The `ignore_errors: yes` parameter is used to ignore errors if the container is not running.

- `- name: Remove the container`: This task removes the Docker container named `regapp-server`. The `ignore_errors: yes` parameter is used to ignore errors if the container doesn't exist.

- `- name: Remove image`: This task removes the Docker image `pranav280499/regapp:latest`. The `ignore_errors: yes` parameter is used to ignore errors if the image doesn't exist.

- `- name: Create container`: This task creates a new Docker container named `regapp-server` from the image `pranav280499/regapp:latest` and exposes port 8080 of the container to port 8082 on the Docker host.

Ensure that the `dockerhost` group is properly defined in your Ansible inventory file, and the Docker daemon is running on the target host. Additionally, ensure that you have appropriate permissions to execute Docker commands on the target host.

2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5914b9ba-6f92-4ff4-b97b-8bc8cda16270)

There is no Containor So we will Get this Error


a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/3b48fb1a-2e2f-42db-b9cd-4e9dafb66c70)

Modify File as
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


b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/80ffef22-0143-4d8a-a878-361a6bfa8d3a)


c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d889bcef-cf63-49b7-ae96-471d91eade80)


d. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/637c3def-c71e-405c-97c3-72e015b62ad4)

## Jenkins CI/CD to deploy on Contaner Using Ansible


1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/ae7cf16b-b390-44f7-86f1-d3b9f66034a9)


Lets make change in index.jsp file


2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a1a0ea02-8fc7-4d2e-9c6e-91fc71838e87)

Lets Build and See


A. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/601a4f20-f210-46bb-ae6d-d954787041ba)


b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/b1fd7199-273e-4061-b5f1-c0911a9ebe1b)



B. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/537a37c9-acca-4a17-ad24-2294afc1b92c)





































