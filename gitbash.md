## Deploy Artifact On Tomcat Server ( Use of Bash )

Open Git Bash on your local machine. You can usually find it in the Start menu on Windows or by searching for "Git Bash".

You should be able to clone a project, make changes, and push those changes to a remote repository using Git Bash on your local machine.

1. **Navigate to Your Desired Location:**
   Use the `cd` command to navigate to the directory where you want to clone the project. For example:
   ```bash
   cd /path/to/your/directory
   ```

2. **Clone the Project:**
   Use the `git clone` command to clone the project from the remote repository. Replace `<repository_url>` with the URL of the remote repository:
   ```bash
   git clone <repository_url>
   ```

3. **Navigate into the Cloned Directory:**
   Use the `cd` command to navigate into the cloned directory:
   ```bash
   cd <cloned_project_directory>
   ```

a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/00b147f6-9970-47c8-9647-7effeb7b1af3)

b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/501d96ba-37e6-4cc0-bb42-61e76d205551)

c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/1cce9758-b6d0-4d4c-9f01-ea05a0c853c1)

4. Use the `cd` command to change directory to the `webapps` directory. If you're unsure of the exact path, you can use the `find` command to locate it. Assuming Tomcat is installed in the default location on Linux, you might run:

   ```bash
   cd /var/lib/tomcat/webapps
   ```

   Replace `/var/lib/tomcat8/webapps` with the actual path to your `webapps` directory if it's different.

5. Once inside the `webapps` directory, you can locate the `index.jsp` file and make changes to it using your preferred text editor. For example, you might run:

   ```bash
   vi index.jsp
   ```


d. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0335bc09-da09-4a45-a65e-9df873520fcd)

e. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c07c83fe-2513-432f-b8f8-4d72765a1f4b)

If you've made changes to files in your project directory and you want to check the status of these changes using Git, you can use the `git status` command. Here's how you can do it:

1. Once you're in your project directory, run the following command to check the status of your changes:

   ```bash
   git status
   ```

   This command will show you the current state of your working directory, including any changes that have been made to files, untracked files, and the branch you're currently on.

2. Look for the `index.jsp` file in the list of modified files. It should appear under the "Changes not staged for commit" section.

3. If you want to stage the changes to be included in the next commit, you can use the `git add` command followed by the filename. For example, to stage changes to `index.jsp`, you would run:

   ```bash
   git add index.jsp
   ```

4. After staging the changes, you can commit them using the `git commit` command. For example:

   ```bash
   git commit -m "Updated index.jsp with changes"
   ```

   Replace the commit message with an appropriate description of the changes you've made.

5. Finally, you can push the changes to your remote repository using the `git push` command. For example:

   ```bash
   git push origin <branch-name>
   ```

By following these steps, you can check the status of your changes, stage them for commit, commit them to your local repository, and push them to your remote repository using Git.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/122cc2e9-0efe-4fc4-9c5b-ca2807f0cdf3)


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/1990f88c-6b29-4b0d-a12b-367c4fa872c8)


![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2fbc2fce-49c9-48f7-a49b-7d49a3e4735d)



   Replace `<branch-name>` with the name of the branch you want to push your changes to, typically `master` or `main`.
   



