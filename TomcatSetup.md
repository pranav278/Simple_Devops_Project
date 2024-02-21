1. Creat New EC2 instance
a.![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f0c10770-e35d-4406-81c5-d5fbde40f66a)
b.![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2771b9ab-8eb1-4a4b-b36a-ccb8e3f31cbb)

c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6aac289e-30ad-426f-8a3e-0f59d5d70f60)

d. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5ec37763-cc76-4a69-b46e-27b8b68d7eb9)

e. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a9885cc6-28c2-4d51-affa-f463987f07b2)

f. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/78493f9d-fb52-40fc-80d2-b81fa1bc495e)


g. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c31f9811-0f05-4175-a960-6446f5a936b3)

h. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/107c63dc-83e9-4b1c-9199-99e32aabcd37)

i. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6198bf50-fc90-43de-a670-dcd39edf5f30)

j. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/407c6efc-9eb6-4190-8711-7dc11f66324f)

k. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/ff502ed7-3ba4-4e68-9abb-00adfb6fe870)

To check where is out Context.xml file

1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/92a062fd-2554-4b00-9653-a45b7ea55038)
2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6068b8fb-8937-443e-9470-6c499bcc2227)
3. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c5fc893e-05c0-40b9-a272-b6994442b422)
4. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/51fbd8bb-4322-48a6-9d33-574b0899e104)


5. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f2c97861-5a60-40ad-b6aa-d3c2277a538f)

After Modificaion need to restart tomcat

1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d81699d8-8228-498a-8dd9-e7c73dbfb080)

2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a1d100b0-d713-4650-aa15-76ae7c9b3186)

Add cred on user.xml

a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/b11e11fc-88e6-4eaf-b9ff-b309539de2d0)

Update users information in the tomcat-users.xml file goto tomcat home directory and Add below users to conf/tomcat-users.xml file
```
 <role rolename="manager-gui"/>
 <role rolename="manager-script"/>
 <role rolename="manager-jmx"/>
 <role rolename="manager-status"/>
 <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
 <user username="deployer" password="deployer" roles="manager-script"/>
 <user username="tomcat" password="s3cret" roles="manager-gui"/>
```
b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/6189bc96-1ac0-4d40-aa52-f00cf15ae54e)

c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2084b072-f396-4fc3-b28d-61d79047bce4)

create link files for tomcat startup.sh and shutdown.sh
```

ln -s /opt/apache-tomcat-<version>/bin/startup.sh /usr/local/bin/tomcatup
ln -s /opt/apache-tomcat-<version>/bin/shutdown.sh /usr/local/bin/tomcatdown
```

d. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/361d91ec-df00-4a4b-b4f4-74c5d38098f2)

e. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/119c8da3-f8d1-495f-b9c6-c5c0a28c0b61)

f. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/65f9558c-3375-4fd5-bd86-2ec69270ae77)






















