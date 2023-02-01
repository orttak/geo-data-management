# VS Code SSH Connection

PC NAME: vm

PC IP: 1.2.3.4

USER NAME: vsCode

**Direct connection on CMD**

$ ssh vsCode@1.2.3.4

**SSH connection on Windows Vs Code**

Ctrl+shift+p >> open command line and find below command

![](../.gitbook/assets/0)

Then

![](<../.gitbook/assets/1 (1)>)

Press “enter” ant then

![](<../.gitbook/assets/3 (1)>)

Press “enter” and you should see below image at lower-left

![](../.gitbook/assets/4)

Press the “Open config” and change your “Host” with your new nickname

After these changes. Prese “ctrt+shift+p” and open your connection and enter your password.

**DOCKER USAGE**

1. **In VM CMD, first we initialize docker image.**

$ docker run --name my\_container_-d --volume target\_volume_/:/home/jovyan/ -p 9998:8888 pangeo/pangeo-notebook:latest jupyter lab --ip 0.0.0.0 $HOME

With above command, we create Docker container which name is geo\_intern from pangeo base image which include most common geospatial python libraries. After this command we have Docker container so we’ll use it for all pipeline. I want to give examples about how we manage the Docker env.

* As you can see, we define container name so if you don’t stop the container or restart computer, you always use this container
* If you don’t see container name with “docker ps”, please start geo\_internt container with “docker start geo\_intern”

**Connecting to Cloud Jupyter env from local machine**

From your local machine CMD, if docker running in Bihter, you should use below command.

$ ssh -L 9998:localhost:9998 [intern@78.188.178.174](mailto:intern@78.188.178.174) #mappingToLocalMachine

first, you should connect with ssh on local machine CMD

$ ssh [intern@78.188.178.174](mailto:intern@78.188.178.174)

Second, you should apply “docker start geo\_intern” method. And then. Back to your local machine and apply “ssh -L 9998:localhost:9998 [intern@78.188.178.174](mailto:intern@78.188.178.174) “ #mappingToLocalMachine

**How we can get Jupyter Ip and Token?**

1. If you restart the container, you can get info with “docker logs geo\_info”

![](<../.gitbook/assets/9 (1)>)

You should apply #mappingToLocalMachine

Raw URL:> [http://127.0.0.1:8888/lab?token=b460e6d3e12abb37ade1a66163123f54e1cab997dffc7862](http://127.0.0.1:8888/lab?token=b460e6d3e12abb37ade1a66163123f54e1cab997dffc7862)

Note: 8888 means container export port. Remember the command when we use to run the container with –p which means port mapping. Sample command> docker run –p 9998:8888 your\_docker\_image

Your local machine URL >

http://127.0.0.1:9998/lab?token=b460e6d3e12abb37ade1a66163123f54e1cab997dffc7862

1. **If container already working, you can get URL info from container.**

Get into container with below command >

$ docker exec -it geo\_intern bash

$ jupyter server list

![](../.gitbook/assets/11)

After ? Mark, you should paste the blog that starts with

**token= f8e75f3830f255914f48ae6b069d74c5c457bd93396f218e**

[http://127.0.0.1:9998/lab?paste\_red\_block](http://127.0.0.1:9998/lab?paste\_red\_block)

Note: we used #mappingToLocalMachine and we defined 9998 as a port of Jupyter lab.

**Update Base Container**
