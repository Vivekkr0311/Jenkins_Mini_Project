# Jenkins_Mini_Project

##Step 1, Install Docker Desktop in your machine

To install Docker Desktop, follow these steps based on your Operating System.

**Windows**

1. Visit the Docker Desktop for Windows Page: https://www.doceker.com/products/docker-desktop
2. Click the "Download for Windows" button, it will download the Doceker Desktop installer
3. Click on the downloaded file and follow the instruction
4. When the installation is complete, Docker Desktop will start automatically

**Mac OS**

1. Visit the Docker Desktop for Mac Page, same link you can use.
   You will just have to select Mac OS.
2. Click the Download Docker Desktop but make sure it you are downloading according to the chip used in your macbook.

3. Once the DMG file is downloaded click on it.
4. You will have a interface where you have to drag and drop the Docker Desktop icon into the Application forlder.
5. Open Docker Desktop from the Application folder.
6. Then Docker Desktop will guide you through the setup process.

**Setting up Jenkins in a Docker image**
1. Create a docker file
2. Add these instruction:
FROM jenkins/jenkins:2.332.3-jdk11
USER root
RUN apt-get update && apt-get install -y lsb-release
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli
USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean:1.25.3 docker-workflow:1.28"
3. Then build the docker image using the below command:
docker build -t myjenkins-blueocean:2.332.3-1 .
4. Then you will have to create a network which will create port forwarding for your docker image to your local machine.
Use the below command here:
docker network create jenkins
5. Check if the network is created, you can use: docker network ls.
This will list down all the network you have created.
6. Now we will run our docker image, and it will use the network you have just created, so that you can access your Jenkins using your local machine.


