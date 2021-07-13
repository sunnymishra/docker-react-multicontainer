In the docker-compose.yml file of "Worker" service, include the Redis host and port as environment variables, Otherwise, you will get a "Calculated Nothing Yet" error message.
	worker:
		environment:
		  - REDIS_HOST=redis
		  - REDIS_PORT=6379
	  
In the docker-compose.yml file of "Client" service, be sure to include the stdin_open: true configuration. Otherwise, you will get a "React App exited with Code 0" error in your terminal when we attempt to start up the application.

  client:
    stdin_open: true
    build:
      dockerfile: Dockerfile.dev
      context: ./client
---------------
Change from below:
	FROM node:alpine

to this:
	FROM node:14.14.0-alpine
---------------
The default.conf should now look like this:

    server {
      listen 3000;
     
      location / {
        root /usr/share/nginx/html;
        index index.html index.htm;
        try_files $uri $uri/ /index.html;
      }
    }
----------------
inside .travis.yml change required for Jest library to work with Create React App
    script:
      - docker run USERNAME/react-test npm test -- --coverage

instead should be:
    script:
      - docker run -e CI=true USERNAME/react-test npm test