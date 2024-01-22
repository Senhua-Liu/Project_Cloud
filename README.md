# Project Software Engineering for the Cloud

PHAM Van Alenn, LIU Senhua
M2 2024 SE1

## Introduction

This project embarks on a journey of exploration and application within the realm of software development, where the subject matter is open-ended, yet guided by a set of prescribed technologies and patterns. The focal points include web services, offering the flexibility of Java or Node.js, Docker for containerization, and Kubernetes for orchestrating multi-containers. The project further delves into diverse options, encompassing cloud deployment, database choices between SQL and NoSQL, and front-end development with frameworks like Angular, React, VueJS, and even extending to Android.

### Starting Point (10/20):
•	Initiate with a single local service by coding a mini application in the language of your choice.
•	Create a Docker image, constructing a Dockerfile for the application.
•	Publish the Docker image to Docker Hub for accessibility.
•	Implement Kubernetes deployment and service by referencing charroux/kubernetes-minikube.

### Enhancements (12/20 to 16/20):
•	Expand functionality by incorporating a local gateway using charroux/kubernetes-minikube#routing-rule-to-a-service-using-ingress or leverage a service mesh with charroux/servicemesh.
•	Integrate a second service, following the guidelines provided in charroux/CodingWithKubernetes.
•	Explore database options, choosing between MySQL and PostgreSQL, either locally or in the cloud.
Cloud Deployment (Optional):
Consider deploying the project in a cloud infrastructure for an additional layer of complexity

# Our Project

First of all we have created our application which is a simple JS service with HTTP requests.
That being done, we have to containairize our application.

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/b091c933-18dc-4afa-a98a-cc696556f54c)

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/e05ddaea-bba7-4f28-88ae-5c719c71910b)

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/7cc4e6e6-b6ef-45ac-afbc-6d029c422407)

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/33ba8d2a-aecd-4a4c-a17e-d24d74d22140)

We add :3000 to bind it to the port 3000 as we wanted to display the app on this port, then we see

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/953cfe87-a0fb-4006-86d1-b71f0d8a1ae1)

Response made out of the GET. 

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/919f525d-c271-413b-b501-5cfa11bd10bc)

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/2b6bda4d-fad0-4e44-8902-4fa2851994ef)

The app functions correctly
We know that the app function locally, but we want to host it on kubernetes so we will remove the container :

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/af46610c-05a4-4ae8-930b-b6c1f7e96414)

Now we need to push the image to DockerHub : 

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/139a4d74-5abc-49b7-a01b-7c0ca852fca0)

The Image has successfully been pushed on DockerHub

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/c6360c5e-93c7-4ef2-961d-16ed2148e699)

While accessing this image we can find the following information :

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/d32bbb5f-31ab-4cd8-981c-fb0bd9cfe1ab)

While checking the tag latest we got the following image layers :

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/9445f028-4129-412f-ad02-cc1decfe11a4)

And so on that define individual instructions.

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/4edd5e25-c9c0-452e-a818-93ff8daa691f)

So this is the image we are going to use if we want to create containers or service development in kubernetes
Now we need to write our kubernetes development yaml

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/6c0a6584-cf3e-4a78-a029-4561ba15182e)

We want a single replica for the pod
Then we create the deploymentservice.yml

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/8ee490ef-899a-4a68-a903-23d9e32022c7)

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/fb3e3941-1998-46a8-aff5-8730b119c152)

Next step is to create and deploy an application in kubernetes
We will use minikube.

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/11725f85-0c02-440f-959b-a56c9d5ba7f7)

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/bfd28997-dac0-431c-a3f9-4cf982370dba)

We verify our kubernetes environment :

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/f0e7ecd9-fb97-4ae1-9843-d94b3f4d9544)

These are already running pods and deployments and svcs which are personal.
We now apply kubectl to the deployment.yml file we created.

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/6e487f5c-ecbf-4528-aacd-57957fbdc9b1)

We now check if it’s correctly created 

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/e3265597-5d85-4971-ba15-3786971031b3)

As expected it has correctly been applied and completed.
As a consequence a pod has been created which is right here : 

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/bac6ee0e-00b2-4a15-8fff-d734eb387e11)

The nodeapp-deployment-5bbf9759db-qmmvr.
In order to access this deployment we need to have a service
So we do the same step with our service.yml file

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/84fd4645-3484-47c9-b4e2-528323a3fdc1)

Our nodeapp-service is bind to the port 5000 mapping to the 31110/TCP.
Now to access our application from outside, we get more information since it’s a minikube. 

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/32740679-18b0-4e22-bc73-8693d215e5fd)

We can find the url to access our application.

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/e29314f5-9388-412e-9c7e-92fb80eae82c)

We paste the matching URL and we can find the information we were seeking for just as the beginning when we ran the app locally. We can even add the methods : 

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/3a475318-a43f-498c-9c75-e436c536027c)

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/440d37d3-2776-4eae-83f6-d5e7b65cdc98)

Now our application is running on a Kubernetes cluster.

### MYSQL INSIDE POD KUBERNETES :

We create the password that will be used during the MySQL server connection inside the dedicated yaml file.

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/e786c36a-9ce6-45a3-960e-51fda3bb2f21)

We define the volumes that will be used by the MySQL server so that we can store the data : 

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/916ecd33-4ba0-42f8-8ded-21e2831d09e6)

We define the MySQL Container that will be deployed on the kubernetes cluster : 

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/06e25f2f-ba06-47fc-9686-8e3d1866926b)

We create a service so that we can access the mysql service inside and outside the cluster :

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/33044f01-31b7-4d35-ace8-5f201facea21)

We verify the configurations previously done :

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/3b30166a-26df-4392-a94d-b3e341c891d5)

According to the Age  criteria we can see the different configurations we’ve deployed (for the MySQL service).

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/4af1bf75-c084-4fb0-a893-7fe253fd92e7)

We create the database and generate the mandatory passwords whether root/user and also we develop the database url which generated as a generic entity.

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/23ea191a-5d1d-4a08-80e4-3b2b990dd74e)

We can see that our configurations were correctly created.

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/2e7ffb93-62fb-4aff-a514-4f415c10e26e)

We create the mysql.yaml file that contains the necessary files to import the mysql service and insert it into a pod.

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/3f5ce33a-84da-458b-b1f4-c096796f6d07)

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/e8ef2f6d-73b9-4e78-ae4e-f97079fe95b7)

Database has correctly been created inside the pods in kubernetes

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/882d16df-43d9-487b-9f52-b536d6ebe16e)

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/8b1b0434-3902-4d84-9141-1c307226f1e4)

We can see that our MySQL service is correctly deployed inside the pod in kubernetes.

Sections Google Labs 

![image](https://github.com/Senhua-Liu/Project_Cloud/assets/73168837/51a6d2b2-ca8a-47e6-b76e-74e9aaf11b17)
