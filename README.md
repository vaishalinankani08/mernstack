# Introduction
This learning path helps you contenarize mernstack movie application,that can be used for managing information about movies.
This application uses mongodb for the database tie,Frontend is in reactjs and backend is in nodejs.
Ubuntu 20.04 compute instance is used for this exercise

![movie_create](https://user-images.githubusercontent.com/77958988/110424432-cc0ab380-80c8-11eb-88e1-d232c3208d17.png)
# Steps
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
 
