## 6. **Integrate Maven with Jenkins*


      1. Setup Maven on Jenkins Server
      2. Setup Environment Variables ( JAVA_HOME, M2, M2_HOME )
      3. Install Maven Plugin
      4. Configure Maven And Java


To navigate to the `/opt` directory and then install Maven from a tar.gz archive, follow these steps:

1. **Navigate to the `/opt` Directory:**
   Open a terminal and use the `cd` command to navigate to the `/opt` directory:

   ```bash
   cd /opt
   ```

2. **Download Maven:**
   You can download the latest version of Maven directly to the `/opt` directory using `wget` or `curl`. For example, using `wget`:

   ```bash
   wget https://downloads.apache.org/maven/maven-3.x.x/binaries/apache-maven-3.x.x-bin.tar.gz
   ```

   Replace `3.x.x` with the latest version number available.

3. **Extract the Archive:**
   Once the download is complete, extract the Maven archive using the `tar` command:

   ```bash
   tar -xvzf apache-maven-3.x.x-bin.tar.gz
   ```

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f5d06644-ee14-4f6f-a13d-cdcae0424096)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/9e9899a0-e839-452b-b0f9-fbb50acbe4c2)

* Moved that file to the maven dir
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/853b0024-ca7f-4c32-b70f-50afd5a0158e)

* If the `mvn` command is not found, it indicates that Maven's bin directory is not included in the system's PATH environment variable. To fix this issue, you need to ensure that the PATH environment variable includes the bin directory of the Maven installation.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/7badc669-6ac5-4de8-83c2-21fae03e49cb)

If you're using Bash as your shell, you can set environment variables in the ~/.bash_profile file. This file is executed for login shells, and it's a common place to set environment variables on Unix-like systems

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d13ac34b-bff4-4a61-b3ee-27f3c977ddd6)

* **Set M2_HOME, M2, and JAVA_HOME:**
   Add the following lines to set the environment variables:

   ```bash
   export M2_HOME=/opt/maven
   export M2=$M2_HOME/bin
   export JAVA_HOME=/path/to/java
   ```

   Replace `/opt/maven` with the actual path to your Maven installation directory and `/path/to/java` with the actual path to your Java installation directory.

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/16569790-6d2f-4668-88b1-914c1e0c99bb)

* To find the Java path on your system, you can use the `find` command to search for the directory containing `jvm` executable. Here's how you can do it:

```bash
sudo find /  -name jvm
```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/87546095-e8f7-4865-8932-671fa652ceb2)

* Check the Changes are Affected or not
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f9fb65b5-6ad4-4fb9-b828-2126cce48e35)

* After making changes to your `.bash_profile` or `.bashrc` file, you need to reload it to apply the changes. You can do this using the `source` command. Here's how:

```bash
source ~/.bash_profile
```


```
source .bash_profile
```
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/bb124730-4675-49ea-a847-3ea9c7cc54b3)

* Now MVN execute from Anywhere

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/9a5d972c-e1a4-4918-8d39-6037c1d463d5)

## Add MAVEN Plugin on Jenkins GUI

1. Add MAVEN integration Plugin 
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4fa2ebd8-203d-4294-bc95-32d72d3c85e7)
2. Add tools configuration for JAVA and Maven
![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2b4bbba2-6b43-46a9-88bd-4619dfd8e46f)

![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f5fcabb4-89a6-4a9d-a52e-a90fb53950c6)

