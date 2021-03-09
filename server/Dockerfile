FROM node:10

# A directory within the virtualized Docker environment
# Becomes more relevant when using Docker Compose later

# Copies package.json and package-lock.json to Docker environment

WORKDIR /opt/app
COPY package*.json ./
COPY . .
RUN CI=true
# Installs all node packages
RUN npm install
# Copies everything over to Docker environment
# Uses port which is used by the actual application
EXPOSE 3000

# Finally runs the application
CMD [ "node", "index.js" ]
