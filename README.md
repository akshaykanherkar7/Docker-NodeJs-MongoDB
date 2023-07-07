# Docker-NodeJs-MongoDB

* ***Build your Node image***
    * **Sample Application**
        * Run following commands on terminal
            ```js
            cd [path to your node-docker directory]
            npm init -y
            npm install ronin-server ronin-mocks
            touch server.js

        * Create **server.js** file and add below code
            ```js
            const ronin = require('ronin-server')
            const mocks = require('ronin-mocks')
            
            const server = ronin.server()
            
            server.use('/', mocks.server(server.Router(), false, true))
            server.start()

      * **Test the Application**
        * Run this command on terminal
            ```js
            node server.js

        * Run this curl request on terminal
            ```js
            curl --request POST \
            --url http://localhost:8000/test \
            --header 'content-type: application/json' \
            --data '{"msg": "testing" }'

            curl http://localhost:8000/test

    * **Docker Setup**
      * Create a **Dockerfile** for Node.js
          ```js
          # syntax=docker/dockerfile:1
    
          FROM node:18-alpine
          ENV NODE_ENV=production
          
          WORKDIR /app
          
          COPY ["package.json", "package-lock.json*", "./"]
          
          RUN npm install --production
          
          COPY . .
          
          CMD ["node", "server.js"]
    
      * Create a **.dockerignore** file
          ```js
          node_modules
    
      * Builde Image
          ```js
          docker build --tag node-docker .
    
      * View local images
          ```js
          docker images
    
      * Tag/Update created Image
          ```js
          docker tag node-docker:latest node-docker:v1.0.0
    
      * Remove docker image
          ```js
          docker rmi node-docker:v1.0.0
          
* ***Run your Image as a Container***
    * Run in detached mode
        ```js
        docker run -d -p 8000:8000 node-docker

    * List running containers
        ```js
        docker ps

    * List all containers (running+non-running)
        ```js
        docker ps -a

    * Restart container by name
        ```js
        docker restart container-name

    * Stop running container
        ```js
        docker stop container-name

    * You can give container-name as you want
        ```js
        docker run -d -p 8000:8000 --name container-name image-name

* ***Use Container for developement***
    * **Local database and containers**
      *  Let’s create our volumes now
          ```js
          docker volume create mongodb
          docker volume create mongodb_config
  
      * Create a network
          ```js
          docker network create mongodb
  
      * 

    
