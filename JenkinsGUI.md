## Step 3:- Setting Up Jenkins GUI

The password for Jenkins is typically not stored in a specific file path like other configurations. Instead, Jenkins manages user authentication using its own user database or an external authentication provider.

However, if you're referring to the Jenkins admin password, which is initially generated during the Jenkins setup wizard, it is usually stored in the Jenkins home directory in a file named `secrets/initialAdminPassword`.

```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```

After retrieving the initial admin password, you can use it to log in to Jenkins for the first time and set up your admin user Account 

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/74b16420-2a88-4657-8b31-2f7ab60454c7)
     
 
After entering Password Click on Continue and We dont need any Plugins currently so Cancel it 
      
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/b4d8cdbd-c875-46ff-99b3-0e81c7d9baa4)

We can  See now Jenkins Home Page
      
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/83703df6-4d65-4a66-b612-8370cd9d5b14)

## **Integrate Github with Jenkins**
      1. Install Git on Jenkins Instance
      2. Install Github Plugin on Jenkins GUI
      3. Configure Git on Jenkins GUI

1. Install Git on Jenkins Instance
   1. Check Git Installed or Not
   ```
   git
   ```
   ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a7e375b4-c765-4f64-9699-a3ee7e6500cb)

   2. Install Git
   ```
   yum install git
   ```
   ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d4a05786-a863-4bb2-914d-882027bfba55)

## Install Github Plugin on Jenkins GUI

To install the GitHub Plugin and configure Git installation in Jenkins, follow these steps:

### Install GitHub Plugin:

1. Navigate to your Jenkins dashboard.
2. Click on "Manage Jenkins" in the left sidebar.
3. Select "Manage Plugins" from the dropdown menu.
4. Go to the "Available" tab.
5. Use the search box to search for "GitHub".
6. Check the checkbox next to "GitHub Plugin".
7. Click on the "Install without restart" button.

### Add Git Installation Configuration:

1. After installing the GitHub Plugin, go back to the "Manage Jenkins" page.
2. Select "Global Tool Configuration" from the list.
3. Scroll down to the "Git installations" section.
4. Click on "Add Git" to add a new Git installation.
5. Enter the following details:
   - **Name:** git
   - **Path to Git executable:** Enter the path to the Git executable. If Git is installed globally, you can usually leave this field empty as Jenkins will search for Git in the system's PATH.
6. Click on "Save" to save the configuration.

Now, Jenkins is configured with the GitHub Plugin and Git installation. You can use Git in your Jenkins jobs for version control and integrate with GitHub repositories.
  
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0018a7e7-56dd-455d-8a0b-15797eee0474)
      
Click on Install without Restart
   
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5f62e98a-47ed-47a8-b022-032ea27502e0)


Click on Apply and SAVE

























