# Introduction
This learning path helps you dockerize mernstack movie application,that can be used for managing information about movies.
This application uses mongodb for the database tie,Frontend is in reactjs and backend is in nodejs.
frondend ie. client is run at port 4000 and  backend i.e. server is run at 3000 port over here.

References:
https://medium.com/swlh/how-to-create-your-first-mern-mongodb-express-js-react-js-and-node-js-stack-7e8b20463e66

Original github link:
https://github.com/samaronybarros/movies-app

Ubuntu 20.04 compute instance is used for this exercise

# Steps for running movie app on ubuntu compute instance
 1.Install nodejs and npm on compute instance following below URL
 
  https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04  
   
 2.Install mongodb on compute instance following below URL 
 
   https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-20-04  

 3.In File ./client/src/api/index.js change the ip address of the server to the public ip address of the compute instance 
  ![axios](https://user-images.githubusercontent.com/77958988/110425452-628ba480-80ca-11eb-8948-098301608ea4.png)
  
 4.Verify that mongodb service is running on compute instance using command "sudo systemctl status mongod"
 
 5.Login to mongodb and create a database with name "cinema" as shown below .
 please follow tutorial : https://www.mongodb.com/basics/create-database
 ![mongologin](https://user-images.githubusercontent.com/77958988/110436551-632c3700-80da-11eb-9351-f1a8d869a50d.png)

 6.Add inbound rules as shown below
 ![inboundrules](https://user-images.githubusercontent.com/77958988/110428489-56561600-80cf-11eb-8e89-892daa7affc8.png)

 7.Run backend and frontend for the movie application with below commands.
 
   client port if required can be changed in file /home/ubuntu/mernstack/client/package.json   
   
   ![clientport](https://user-images.githubusercontent.com/77958988/110437936-e7cb8500-80db-11eb-8d59-5ffb30b5cbe0.png)
   
   
   server port if required can be changed in file /home/ubuntu/mernstack/server/index.js  
   ![serverport](https://user-images.githubusercontent.com/77958988/110438427-5f99af80-80dc-11eb-9570-20394bdba190.png)

 
  ```
  #run client ( port 4000)
  cd client
  npm start
  #run server ( port 3000)
  cd server
  node index.js
  ```
 8.Open the application GUI in webbrowser http://compute-instance-public-ip:4000
# Steps for running dockerized  movie app using host network
 Lets see how to dockerize & run the movie application along with containerized mongodb.
 
1.Download mongodb docker image from DockerHub
  
  ```
ubuntu@ip-172-31-94-114:~/up$ sudo docker pull mongo
Using default tag: latest
latest: Pulling from library/mongo
92dc2a97ff99: Pull complete
be13a9d27eb8: Pull complete
c8299583700a: Pull complete
f61ed17142e4: Pull complete
bed7676d225b: Pull complete
ba553bcfc69c: Pull complete
e5046b6c236f: Pull complete
80191acfded2: Pull complete
d41d63fc76cc: Pull complete
5605b8c2e9f7: Pull complete
e8b16825b485: Pull complete
3d40ccce1309: Pull complete
Digest: sha256:51f6fdbfc622d91e276ade7e6cf6491aa36ff2bd9b158dadb732f9e4a05f33ad
Status: Downloaded newer image for mongo:latest
docker.io/library/mongo:latest
  ```
2.Stop mongodb service running on compute instance using below command
 ```
 sudo systemctl stop mongod
 sudo systemctl status mongod
 ```
 
3.run mongo db container  and create database with name cinema as shown below
````
ubuntu@ip-172-31-94-114:~/mernstack/server$ sudo docker run -it --name=mongo -d --network host --expose 27017  mongo:latest
fe656477549aac046c9e19c2df7e1094c7048341eaf3fac52d7094fb2277f19f
ubuntu@ip-172-31-94-114:~/mernstack/server$ sudo docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                      NAMES
fe656477549a   mongo:latest   "docker-entrypoint.s…"   17 seconds ago   Up 16 seconds   0.0.0.0:27017->27017/tcp   mongo
ubuntu@ip-172-31-94-114:~/mernstack/server$ sudo docker exec -it fe656477549a bash
root@fe656477549a:/# ls
bin   data  docker-entrypoint-initdb.d  home        lib    media  opt   root  sbin  sys  usr
boot  dev   etc                         js-yaml.js  lib64  mnt    proc  run   srv   tmp  var
root@fe656477549a:/#
root@fe656477549a:/#
root@fe656477549a:/# mongo
MongoDB shell version v4.4.4
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("5a346343-74e1-472a-846d-4c86c8d1f505") }
MongoDB server version: 4.4.4
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
        https://docs.mongodb.com/
Questions? Try the MongoDB Developer Community Forums
        https://community.mongodb.com
---
The server generated these startup warnings when booting:
        2021-03-08T18:07:01.082+00:00: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem
        2021-03-08T18:07:01.858+00:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
---
---
        Enable MongoDB's free cloud-based monitoring service, which will then receive and display
        metrics about your deployment (disk utilization, CPU, operation statistics, etc).

        The monitoring data will be available on a MongoDB website with a unique URL accessible to you
        and anyone you share the URL with. MongoDB may use this information to make product
        improvements and to suggest MongoDB products and deployment options to you.

        To enable free monitoring, run the following command: db.enableFreeMonitoring()
        To permanently disable this reminder, run the following command: db.disableFreeMonitoring()
---
>
---
> show databases;
admin   0.000GB
config  0.000GB
local   0.000GB
> use cinema
switched to db cinema
> exit
bye
root@ip-172-31-94-114:/# exit
exit

````

4.Write Dockerfile for frontend i.e. client [Dockerfile](https://github.com/vaishalinankani08/mernstack/blob/main/client/Dockerfile) and place it in client folder.

5.Write Dockerfile for backend  i.e. server [Dockerfile](https://github.com/vaishalinankani08/mernstack/blob/main/server/Dockerfile) and place it in server folder.

6.Create docker image for client
````
ubuntu@ip-172-31-94-114:~/mernstack/client$ sudo docker build -t mernstack/client:1.0.0 .
````
7.Create docker image for server
````
ubuntu@ip-172-31-94-114:~/mernstack/server$ sudo docker build -t mernstack/server:1.0.0 
````
8.verify that both client and server images are created as shown below
````
ubuntu@ip-172-31-94-114:~/mernstack/server$ sudo docker images
REPOSITORY         TAG       IMAGE ID       CREATED         SIZE
mernstack/server   1.0.0     bffb9dd45350   7 seconds ago   921MB
mernstack/client   1.0.0     cab9f08e0846   4 minutes ago   1.13GB
mongo              latest    bbfd3e575f12   4 days ago      449MB
node               10        711c143a39dd   12 days ago     910MB
````
9.Deploy docker containers for client and server as shown below
````
ubuntu@ip-172-31-94-114:~/mernstack$ sudo docker run -it --name=server -d --network host --expose 3000  mernstack/server:1.0.0
690e01123932aba721cfc617bcec5bb1eacc1a386ffc59724a43cb6bd344d3ac
ubuntu@ip-172-31-94-114:~/mernstack$ sudo docker run -it --name=client -d --network host --expose 4000  mernstack/client:1.0.0
09fa6b9b898c0f309e6f50b5cfd82154b8f5c0bfda71f522333a77ca57103900
ubuntu@ip-172-31-94-114:~/mernstack$ sudo docker ps -a
CONTAINER ID   IMAGE                    COMMAND                  CREATED          STATUS          PORTS     NAMES
09fa6b9b898c   mernstack/client:1.0.0   "docker-entrypoint.s…"   9 seconds ago    Up 9 seconds              client
690e01123932   mernstack/server:1.0.0   "docker-entrypoint.s…"   20 seconds ago   Up 20 seconds             server
82552720fb81   mongo:latest             "docker-entrypoint.s…"   5 minutes ago    Up 5 minutes              mongo
````
10.Open the application GUI in webbrowser http://compute-instance-public-ip:4000
![movieapp screen](https://user-images.githubusercontent.com/77958988/110434953-6f16f980-80d8-11eb-8711-240f3894b94b.png)

11. Click on "Create Movie" to craete a entry for movie
 ![movie_create](https://user-images.githubusercontent.com/77958988/110424432-cc0ab380-80c8-11eb-88e1-d232c3208d17.png)
 
12. Click on "List Movies" to list all movies
![movie_list](https://user-images.githubusercontent.com/77958988/110435490-16942c00-80d9-11eb-8d1d-093d0d5d4cec.png)


