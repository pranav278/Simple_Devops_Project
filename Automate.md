## Step 8: Automate Build and Deployment on docker Container

* Make the Changes in Jenkins ( so it will creat imange and Container Automatically )
To add these steps as post-build actions in a Jenkins job, you can follow these steps:

1. **Navigate to Job Configuration**:
   - Go to the Jenkins dashboard.
   - Click on your desired job.

2. **Configure Post-build Actions**:
   - Scroll down to the "Post-build Actions" section.
   - Click on the "Add post-build action" dropdown and select "Execute shell" or "Execute Windows batch command" depending on your operating system.

3. **Enter Commands**:
   - In the command input area, enter the following commands:
     ```bash
     cd /opt/docker
     docker build -t regapp:v1 .
     docker run -d --name registerapp -p 8087:8080 regapp:v1
     ```

4. **Save Configuration**:
   - Once you've entered the commands, scroll down to the bottom of the page and click on the "Save" or "Apply" button to save your Jenkins job configuration.

These steps will ensure that after your Jenkins job is executed, it will navigate to the `/opt/docker` directory, build the Docker image tagged as `regapp:v1`, and then run a container based on that image with the specified options.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/38fe4f9c-9f2d-4276-b717-72e098de5120)

* Now See Image is Created or not 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/8f67efea-375a-4c11-80e8-d745401a473e)

* Here, our now tomcat server is up

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2d461242-4484-4892-b6f4-3b989b3b1bf6)

* Now lets make Change and Pull through Bash 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/36f3fbd8-3cb9-4b69-8f86-659a091f0274)

* Make Change in index.jsp

1. **Check Git Status**:
   ```bash
   git status
   ```
   This command shows the current status of your Git repository, including any changes that have been made.

2. **Stage Changes**:
   ```bash
   git add .
   ```
   This command stages all changes in the current directory for the next commit. The `.` indicates that you want to stage all changes. If you only want to stage specific files, you would specify them instead of `.`.

3. **Commit Changes**:
   ```bash
   git commit -m "Your commit message here"
   ```
   This command commits the staged changes to the local repository. Replace `"Your commit message here"` with a brief description of the changes you're committing.

4. **Push Changes to Remote Repository**:
   ```bash
   git push origin master
   ```
   This command pushes your committed changes from the local repository to the remote repository (`origin`) on the `master` branch. If you're working on a different branch, you would replace `master` with the name of your branch.



![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2f774279-4afc-4ef1-8af3-634e698afc06)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/346f1fb0-6d5a-4649-a9d2-9828568eaad2)


* See Build gets automatic trigger

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/775b62fb-49ac-4c32-a9cf-f7c58653ad8d)

* lets try it out manually, will see why gets error

Let's Build Docker image 
```
docker build -t regapp:v1
```


- `docker build`: This is the command to build a Docker image.
- `-t regapp:v1`: This part of the command specifies the tag for the image being built. In this case, the tag is `regapp:v1`. Tags are used to label and identify different versions or variations of Docker images. `regapp` seems to be the name of the application, and `v1` indicates that this is version 1 of the application.



```bash
docker run --name registerapp -p 8087:8080 regapp:v1
```

This command will run a Docker container based on the `regapp:v1` image with the following options:

- `--name registerapp`: Assigns the name `registerapp` to the container.
- `-p 8087:8080`: Maps port 8080 from the container to port 8087 on the host, allowing you to access the application running inside the container via `http://localhost:8087`.
- `regapp:v1`: Specifies the name of the Docker image to use for creating the container, in this case, `regapp:v1`.


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/45bc9344-8cde-4d72-b85f-6360a22bb791)

* this is due to same container name

* So lets , Modify Configuration 
```
cd /opt/docker;
docker build -t regapp:v1 .;
docker stop registerapp;
docker rm registerapp;
docker run -d --name registerapp -p 8087:8080 regapp:v1
```

1. `cd /opt/docker;`: Changes the current directory to `/opt/docker`.
2. `docker build -t regapp:v1 .;`: Builds a Docker image named `regapp:v1` using the Dockerfile found in the current directory (`.`).
3. `docker stop registerapp;`: Stops the Docker container named `registerapp`, if it is currently running.
4. `docker rm registerapp;`: Removes the Docker container named `registerapp`, if it exists.
5. `docker run -d --name registerapp -p 8087:8080 regapp:v1`: Runs a new Docker container in detached mode (`-d`) with the name `registerapp`, mapping port 8087 on the host to port 8080 in the container, based on the `regapp:v1` image.

* Now build and see

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/249311f0-9756-4025-83ba-06b472c50830)








