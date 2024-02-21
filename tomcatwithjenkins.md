## Integrating Apache Tomcat with Jenkins

- Integrating Apache Tomcat with Jenkins allows you to deploy Java web applications directly from Jenkins to Tomcat servers. Here's a basic outline of the integration process:

Add the "Deploy to Container Plugin" in Jenkins:

1. **Open Jenkins Dashboard:**
   Open your web browser and navigate to your Jenkins server's URL. Log in to the Jenkins dashboard with your credentials.

2. **Go to Manage Jenkins:**
   Click on "Manage Jenkins" from the left-hand sidebar. This will take you to the Jenkins management page.

3. **Access Plugin Manager:**
   In the "Manage Jenkins" page, click on "Manage Plugins." This will open the Jenkins Plugin Manager.

4. **Navigate to Available Plugins:**
   In the Plugin Manager, you'll find different tabs. Click on the "Available" tab to view the list of available plugins that can be installed.

5. **Search for "Deploy to Container Plugin":**
   In the search box, type "Deploy to Container Plugin" or simply "Deploy to Container". The plugin should appear in the filtered list.

6. **Select Plugin for Installation:**
   Find the "Deploy to Container Plugin" in the list of available plugins and check the checkbox next to it.

7. **Install Plugin:**
   After selecting the "Deploy to Container Plugin", scroll down to the bottom of the page and click on the "Install without restart" button. This will begin the installation process.

8. **Wait for Installation:**
   Jenkins will download and install the plugin. This may take a few moments depending on your network speed and server performance.

9. **Verify Installation:**
   Once the installation is complete, you'll see a message indicating that the plugin was installed successfully.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/3c371208-d207-452d-b33e-913dbb27c793)

To configure Tomcat credentials in Jenkins using the Global Credentials feature, follow these steps:

1. **Access Jenkins Dashboard:**
   Log in to your Jenkins server and navigate to the Jenkins dashboard.

2. **Go to Manage Jenkins:**
   Click on "Manage Jenkins" from the sidebar menu. This will take you to the management page.

3. **Access Credentials:**
   In the "Manage Jenkins" page, click on "Manage Credentials". This will open the Credentials page where you can manage various types of credentials.

4. **Add Global Credentials:**
   In the Credentials page, click on "Global credentials (unrestricted)" from the left-hand side menu.

5. **Add Credentials:**
   Click on the "Add Credentials" link to add a new credential.

6. **Select Credentials Kind:**
   Choose the type of credentials you want to add. Since you're adding Tomcat credentials, you might select "Username with password".

7. **Enter Credentials Information:**
   Fill in the following details:
   - **Username:** Enter the username for the Tomcat user (e.g., `deployer`).
   - **Password:** Enter the password for the Tomcat user (e.g., `deployer`).
   - **ID:** Optionally, you can specify an ID for the credentials. This ID is used to reference the credentials in Jenkins configurations.

8. **Scope Configuration:**
   Set the appropriate scope for the credentials. Since you want to use these credentials globally, you should leave the scope as "Global (Jenkins, nodes, items, all child items, etc)".

9. **Click on "OK" or "Create":**
   After entering the required information, click on "OK" or "Create" to save the credentials.

10. **Verify Credentials:**
    Once you've created the credentials, you can verify that they appear in the list of global credentials. You should see the credentials you just added listed there.

By configuring Tomcat credentials in Jenkins using the Global Credentials feature, you can securely manage authentication information for Tomcat servers and use them in your Jenkins jobs for deploying applications or performing other tasks.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/97af7c58-be2d-4f9e-b774-0532d1c36184)

c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/3ad897ba-3b4e-4953-948f-8946f8e5ff2b)

d. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bb374b41-230e-46b4-bb77-9c0856475df9)

To create your first Maven job in Jenkins for deploying a project, named "Deployment of Job", follow these steps:

1. **Access Jenkins Dashboard:**
   Log in to your Jenkins server and navigate to the Jenkins dashboard.

2. **Create a New Job:**
   Click on the "New Item" or "New Job" link on the Jenkins dashboard. This will start the process of creating a new job.

3. **Enter Job Details:**
   - Enter the name "Deployment of Job" in the "Enter an item name" field.
   - Select "Maven Project" as the project type.
   - Click "OK" to proceed.

4. **Configure Maven Project:**
   You will be directed to the configuration page for the Maven project. Here's how to configure it:

   - **General:**
     - Description: (Optional) Add a description for your Maven job.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/41ab6fb1-1440-4117-8ff7-f6022ddeb219)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a66c84b4-fa84-4f02-bb7b-d2b813e4938b)

5. **Configure Source Code Management:**
   Scroll down to the "Source Code Management" section.

6. **Choose Git:**
   Select "Git" as the source code management system. This will reveal options specific to configuring Git.

7. **Add Repository URL:**
   In the "Repository URL" field, enter the URL of your Git repository.

8. **Leave Credentials Empty:**
   Since your Git repository is public and doesn't require credentials, leave the "Credentials" field empty. Jenkins will automatically handle authentication for public repositories.

9. **Branches to Build (Optional):**
   If you want to build specific branches, you can specify them in the "Branches to build" field. Otherwise, Jenkins will build the default branch (usually `master`).

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5584bbd0-22eb-48b1-b959-20a96c11ed09)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f6743744-54a0-4396-bc6c-e2af588b5ba7)

10. **Configure Build Environment:**
   Scroll down to the "Build" section and click on the "Add build step" dropdown.

11. **Set Root POM:**
   In the "Root POM" field, enter the path to your `pom.xml` file. If your `pom.xml` file is located in the root directory of your project, you can simply enter `pom.xml`.

12. **Set Goals and Options:**
   In the "Goals and options" field, enter the Maven goals and options you want to execute during the build process. For example, you can enter `clean install` to clean the project and then install dependencies and package the project into a JAR or WAR file.

By configuring the build environment with the specified `pom.xml` file and Maven goals and options, Jenkins will execute the Maven build according to your project's requirements. This setup allows for flexibility in configuring the Maven build process within Jenkins.
   
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/71a5d067-ea3c-436d-8dcd-164ad8f98884)

To configure Jenkins to deploy the WAR files to a remote Tomcat server as a post-build action, follow these steps:

1. **Access Jenkins Dashboard:**
   Log in to your Jenkins server and navigate to the Jenkins dashboard.

2. **Select Your Maven Project:**
   Click on the "Deployment of Job" Maven project you've created to edit its configuration.

3. **Configure Post-Build Actions:**
   Scroll down to the "Post-build Actions" section.

4. **Add Post-Build Action:**
   Click on the "Add post-build action" dropdown and select "Deploy war/ear to a container".

5. **Specify WAR File:**
   - In the "WAR/EAR files" field, enter `**/*.war`. This specifies that Jenkins should deploy all WAR files found in the project workspace.

6. **Set Context Path:**
   - Leave the "Context path" field blank. This means that Tomcat will use the default context path for the deployed application.

7. **Select Tomcat Container:**
   - Choose "Tomcat 8.x Remote" from the "Containers" dropdown. This specifies that Jenkins will deploy the WAR files to a remote Tomcat server.

8. **Specify Tomcat Credentials:**
   - In the "Credentials" dropdown, select the credentials you created earlier for authenticating with the Tomcat server.

9. **Enter Tomcat URL:**
   - In the "Tomcat URL" field, enter the URL of your Tomcat server where you want to deploy the WAR files (e.g., `http://your_tomcat_server:8080`). Make sure to replace `your_tomcat_server` with the actual hostname or IP address of your Tomcat server.

10. **Save Configuration:**
    Once you've configured the post-build actions, click on the "Save" or "Apply" button to save the changes.

11. **Run the Job:**
    You can now run the Maven job by clicking on the "Build Now" button. Jenkins will start the build process and deploy the WAR files to the specified Tomcat server as a post-build action.

By following these steps, Jenkins will automatically deploy the WAR files to the remote Tomcat server after a successful build, streamlining the deployment process for your Maven project.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d0b4c026-ce1e-43ed-b4c1-02c6e7618af7)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c5c74416-c8b2-4641-a673-4979783071e9)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2c150f51-2252-4359-a9f3-c4f0707d53ea)

Once the Jenkins job runs and successfully deploys the WAR file to the Tomcat server, you should be able to see the deployed application listed in the Tomcat Web Application Manager.

To access the Tomcat Web Application Manager:

1. Open a web browser and navigate to the Tomcat Manager URL. This is typically `http://your_tomcat_server:8080/manager/html`.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/82d7ba7a-c18a-4f9e-9308-56c606cec5e1)

* Output :- 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/738c777a-3633-483e-9a8a-16708f2fab36)

















