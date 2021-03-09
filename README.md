# Introduction
This learning path helps you contenarize mernstack movie application,that can be used for managing information about movies.
This application uses mongodb for the database tie,Frontend is in reactjs and backend is in nodejs.
Ubuntu 20.04 compute instance is used for this exercise

![movie_create](https://user-images.githubusercontent.com/77958988/110424432-cc0ab380-80c8-11eb-88e1-d232c3208d17.png)
# Steps for movie app
 1.Install nodejs and npm on compute instance following below URL
  https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04  
   
 2.Install mongodb on compute instance following below URL 
   https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-20-04  

 3.In File ./client/src/api/index.js change the ip address of the server to the public ip address of the compute instance 
  ![axios](https://user-images.githubusercontent.com/77958988/110425452-628ba480-80ca-11eb-8948-098301608ea4.png)
 
 4.In File ./client/src/api/index.js change the ip address of the server to the public ip address of the compute instance 
 
 5.Verify that mongodb service is running on compute instance using command "sudo systemctl status mongod"
 
 6.Login to mongodb and create a database with name "cinema" as shown below .
 please follow tutorial : https://www.mongodb.com/basics/create-database
 ![mongologin](https://user-images.githubusercontent.com/77958988/110428309-1131e400-80cf-11eb-979a-16ba36f2201b.png)

 7.Add inbound rules as shown below
 ![inboundrules](https://user-images.githubusercontent.com/77958988/110428489-56561600-80cf-11eb-8e89-892daa7affc8.png)

 8.Run backend and frontend for the movie application with below commands
  ```
  #run client ( port 4000)
  cd client
  npm start
  #run server ( port 3000)
  cd server
  node index.js
  ```
 9.Open the application GUI in webbrowser http://compute-instance-public-ip:4000
# Steps for running containerized  movie app
 Lets see how to containerize the movie application along with containerized mongodb.
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
    
 
