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

a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/ad071d5e-e173-4ab2-b403-d812466d12c8)

Able to Connect with docker but not ansible because keys are not present

1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5807122c-d524-4231-a8f2-dd9eaa30b76e)

2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a32b3867-3c6b-4d8a-9edd-51e5df5af8ae)

Now it showing for both because we copied both the keys

Now Create Ansible Playbook

a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5b024e08-9666-4a24-8170-41016fb07933)

b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/a0b10298-44f5-46ec-b6a8-779d893a996e)

## Copy Imange on the dockerhub

1. Create Dockerhub acccount

2. To commit your image to Dockerhub you need login account through ansible-server

login to dockerhub

3. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/21d1aec4-cb34-4df5-bb16-d2a54138eed1)

We cannot direclty Push to Dockerpush because it could not Reconize account


a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/55ea2d1e-7676-41b1-bf32-bb6fe89ce90e)


b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/58d975ac-184f-44c6-a010-c3aefef911eb)


c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c2272f14-9ebf-4e3f-bbc1-dd3bea3926ea)


d. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d5ec559f-b7f3-4652-93b3-fc1798f0646d)

## Jenkins Job to Build an Imange onto Ansible

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

a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0d34331b-34fb-4029-8b82-963693ad6ed2)

Now check the file


b. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/c0b173dd-c0e9-489c-aaef-f3a795856dd5)

Limits


1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/3070a439-d610-4ca0-9b74-05e2dd6ca5ff)


2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/624a0674-9467-4757-8c74-cd583fcd6d18)


Enable Poll SCM alos


a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/ba4ca1be-b7e5-4172-a59d-0c52e254efb1)

Lets Make Changes in index.jsp file through GIT 


1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2e62042d-89fc-4c09-94a6-e96b2fd853aa)


2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/4f17365b-7ae0-41dd-8cec-5c4b244a7cf8)


3. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/be80efd1-1953-4a6a-a62b-ead553fbdbff)


4. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/9f175a4a-053c-49ae-8f6d-e3af07cc73d3)

## Create Container on Dockerhost using Ansibleplaybook
```
---
- hosts: dockerhost

  tasks:
  - name: create container
    command: docker run -d --name regapp-server -p 8082:8080 pranav280499/regapp:latest
```


1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/f32578eb-e405-4558-b51e-1901e91dd3af)


2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/d52dd5e0-83ab-4d49-b234-5ff6a571b043)


3. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/12b8b7f2-00f3-43dc-8c79-690c51338875)

login to Dockerhost

Delete all the images and Container of Dockerhost


1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/60a11b68-cb0d-426e-a486-d9c9ceebd801)


2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/35a5d61a-7b61-4f66-a6dd-8aed534e0d16)

Now lets try to pull image from dockerhub as a ansadmin using ansibleplaybook


a. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/1e8ab9ec-7481-4823-ae74-dc7100279aec)

Its Giving Error Dure to Permission


b.![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/543c37ff-5efe-4f30-8423-f96fa7a3ba6f)


c. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/5f006298-fda8-4ba9-ade6-44c6dc89af9a)

Now check image and Container Created or not


1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/16dc25b1-8df2-4888-b4e1-7646b3f9d3d0)


2. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/2643a7e3-ffc9-42db-80c5-fc4816def8a4)


3. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/eae8b0a0-d754-44aa-a3ca-b9517f3d7a69)

If We run playbooks once again, Container alredy Present lets see how to Resolve this issue


1. ![image](https://github.com/pranav278/Simple_Devops_Project/assets/84725860/0468a1c3-e972-4cef-9b5b-71a2834bd211)

'''
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





































