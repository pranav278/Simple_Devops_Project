## Setting Up Jenkins GUI


      1. Password for Jenkins Stored in this Path : /var/lib/jenkins/secrets/initialAdminPassword
      ```
      cat /var/lib/jenkins/secrets/initialAdminPassword
      ```
      ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/74b16420-2a88-4657-8b31-2f7ab60454c7)
      2. After entering Password Click on Continue and We dont need any Plugins currently so Cancel it 
      ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/b4d8cdbd-c875-46ff-99b3-0e81c7d9baa4)

      - We can  See now Jenkins Home Page
      ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/83703df6-4d65-4a66-b612-8370cd9d5b14)

5. **Integrate Github with Jenkins**
      1. Install Git on Jenkins Instance
      2. Install Github Plugin on Jenkins GUI
      3. Configure Git on Jenkins GUI

## 1. Install Git on Jenkins Instance
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

## 2. Install Github Plugin on Jenkins GUI
   1. Go to the Highlighted Path to Add Pluging
   ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0018a7e7-56dd-455d-8a0b-15797eee0474)
      
   Click on Install without Restart
   2. Add the Git Installation Configuration 
   ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5f62e98a-47ed-47a8-b022-032ea27502e0)

   Click on Apply and SAVE

























