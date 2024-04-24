# MauliBhavsar57.github.io
To run Three Tier Application using Docker, we need to first create a Full Stack Project. We can use any of our Full Stack Project but if we don’t have one then we can use someone else project also. Here, I have used a very easy simple project on GitLab.This project is made using HTML, CSS, JavaScript, Express and MongoDB.<br>
First you need to clone the Project Repository from the link using command:
git clone https://gitlab.com/nanuchi/developing-with-docker <br>
To run a Three Tier Application, we need to run three Docker Containers simultaneously. So, it is necessary to run all these containers inside a network to avoid their interaction with other containers. 
So, Network can be created by using the following command after starting the Docker Engine with name mongo-network
![2](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/c9150e68-181b-41e3-aabd-afa59feeffb1)
<br>
You can see all the networks using the command: docker network ls. Now, we need to pull the image of MongoDB from DockerHub and make container from it. Then we need to run this container in the network to access MongoDB Database using Docker Container.<br>
![3](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/4e37c8f0-4036-4bb5-a3f2-98ff411ec0d2) <br>
To pull MongoDB image from DockerHub and run it as container we need to execute the command
![4](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/f4802c4c-1efd-4a04-b3de-7e9a4de7dde0) <br>
Here, the mongo image will be automatically pull from the DockerHub to run the Container in detachable mode with name mongodb in the network mongo-network. The Container will be running on the default 27017 port. You can check all the running containers using command docker ps. Environment Variables Username and Password are also passed to run the container. Similarly, we will be creating another container of Express by pulling its image from the DockerHub.<br>
Express Container can be run by using the follow command
![5](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/5dbafe52-82a2-45f6-ac57-355c4e8551e1) <br>
Here, the container with name mongo-express is made to connect the MongoDB Database with the Frontend of the project in Docker. As explained above, the container will run on 8081 port. The environment variables Username and Password are passed of the MongoDB to access the Database along with the container name of the MongoDB in the Server Environment variable. The container will be running on the same network as the above container. <br>
Now, open the link in your browser localhost:8081 and create two databases my-db and user-accounts
![6](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/64ac4096-3459-4214-aec1-7a891fee4883) <br>
Creating these two databases is necessary as the Frontend will be requiring these while running. Also, we need to change the MongoDB URL mentioned in the server.js file as we will be running MongoDB using Docker instead of Local Machine.<br>
Naviagate to the server.js file in the project and replace mongoUrlLocal and mongoUrlDocker with the fol!lowing value 
(https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/c5adc491-1572-4c15-9226-2b396ebd1d2b)
<br>
create a new Dockerfile inside the app folder of the project with the following commands <br>
FROM node WORKDIR /app COPY . . ENV MONGO_DB_USERNAME=admin ENV MONGO_DB_PWD=password RUN npm install EXPOSE 3000 CMD ["node", "server.js"] 
![9](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/99428cec-c6e7-4ea0-a332-1809617c8f23) <br>
Open the CMD Terminal inside the app folder of the project and run the command
![8](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/9513b697-b609-4f02-8186-87d3d50630d0) <br>
To run the Image as a Docker Container run the command
![10](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/c2cfd998-3ee7-4ad7-a443-c013f038c637) <br>
![11](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/1882e261-1fb1-44e7-88cc-ffae7f1c59e1)
<br>
Now, open the following link on you browser localhost:3000 and you will see a webpage running.
![12](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/fe110185-cfa2-4412-89e0-c9a01ac0fb6b)
<br>
To push the Docker Image of the project run the command
![image](https://github.com/MauliBhavsar57/MauliBhavsar57.github.io/assets/109329874/02f89934-fccd-4396-b120-f6b05856ea2b)
<br>
