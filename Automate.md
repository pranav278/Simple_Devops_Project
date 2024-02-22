## Automate Build and Deployment on docker Container

Make the Changes in Jenkins ( so it will creat imange and Container Automatically )
```
cd /opt/docker;
docker build -t regapp:v1 .;
docker run -d --name registerapp -p 8087:8080 regapp:v1
```

a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/38fe4f9c-9f2d-4276-b717-72e098de5120)

Now See Image is Created or not 

b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/8f67efea-375a-4c11-80e8-d745401a473e)

c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2d461242-4484-4892-b6f4-3b989b3b1bf6)

Now lets make Change and Pull through Bash 

1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/36f3fbd8-3cb9-4b69-8f86-659a091f0274)

Make Change in index.jsp

a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2f774279-4afc-4ef1-8af3-634e698afc06)

b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/346f1fb0-6d5a-4649-a9d2-9828568eaad2)

Build gets automatic trigger

1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/775b62fb-49ac-4c32-a9cf-f7c58653ad8d)

lets try it out manually, will see why gets error


a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/45bc9344-8cde-4d72-b85f-6360a22bb791)

thisis due to same container name
Modify Configuration 
```
cd /opt/docker;
docker build -t regapp:v1 .;
docker stop registerapp;
docker rm registerapp;
docker run -d --name registerapp -p 8087:8080 regapp:v1
```
Now build and see

1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/249311f0-9756-4025-83ba-06b472c50830)








