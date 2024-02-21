## 6. **Integrate Maven with Jenkins*


      1. Setup Maven on Jenkins Server
      2. Setup Environment Variables ( JAVA_HOME, M2, M2_HOME )
      3. Install Maven Plugin
      4. Configure Maven And Java

A. Setup MAVEN
1. Install maven using tar file
Go to the link Copy the tar file  : https://maven.apache.org/download.cgi
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f5d06644-ee14-4f6f-a13d-cdcae0424096)

2. Extract this file
```
tar -xvzf pkgname
```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/9e9899a0-e839-452b-b0f9-fbb50acbe4c2)

3. Moved that file to the maven dir
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/853b0024-ca7f-4c32-b70f-50afd5a0158e)

4. Because of this we need to set enviroment variable
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/7badc669-6ac5-4de8-83c2-21fae03e49cb)

5. For Setting up ENV variable we need bash_Profile file
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d13ac34b-bff4-4a61-b3ee-27f3c977ddd6)

6. Modify with 
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/16569790-6d2f-4668-88b1-914c1e0c99bb)

7. How to find JAVA path
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/87546095-e8f7-4865-8932-671fa652ceb2)

8. Check the Changes are Affected or not
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f9fb65b5-6ad4-4fb9-b828-2126cce48e35)

9. Reload the file once
```
source .bash_profile
```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bb124730-4675-49ea-a847-3ea9c7cc54b3)

10. Now MVN execute from Anywhere

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/9a5d972c-e1a4-4918-8d39-6037c1d463d5)

B. Add MAVEN Plugin on Jenkins GUI

1. Add MAVEN integration Plugin 
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4fa2ebd8-203d-4294-bc95-32d72d3c85e7)
2. Add tools configuration for JAVA and Maven
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2b4bbba2-6b43-46a9-88bd-4619dfd8e46f)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f5fcabb4-89a6-4a9d-a52e-a90fb53950c6)

