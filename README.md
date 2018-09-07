# Nginx as reverse proxy with Docker Compose

This repository shows you how to use Nginx as a reverseproxy and router to access muliple docker containers.

## Description

If you look at an application that is made up of several docker containers, than it would be useful if you could access all containers via http and one root url. In this situation a the Gateway pattern is useful.

To introduce a simple example to show you how you can use Nginx as a reverse proxy and gateway router, we use two Asp.Net Core Apis, an Apache and a Nginx behind a reverse proxy.

### Asp.Net Core Apis

- apione can be found in folder apione.
To create the docker image switch to folder apione and run ```docker build -t apione . ```
- apitwo can be found in folder apitwo.
To create the docker image switch to folder apitwo an run ```docker build -t apitwo . ```

### Reverse Proxy

The sources for the reverse proxy are located in the folder reverse proxy.
To create the image swicth to folder reverseproxy and run ```docker build -t reverseproxy . ```
Take a look at [nginx.conf](reverseproxy/nginx.conf) to see how nginx is configured.
You see that Nginx is running on port 8080 and that the other containers are accessible through subpates
- Apache -> localhost:8080/apache
- apione -> localhost:8080/apione
- apitwo -> localhost:8080/apitwo
- Nginx -> localhost:8080 

### Docker Compose

Switch to root directory and run ```docker-compose up``` to start all containers.
Take a look at the [docker-compose.yml](docker-compose.yml) file.
Here you cann see the description of the services.

Now that the containers are up and running, open your browser and go to ```localhost:8080```.
You see the startup page of Nginx.
Then navigate to ```localhost:8080/apache```, you see the startup page of the running Apache.
After that, navigate to ```localhost:8080/apione/api/values```, you se the response of the api request.
At the end, navigate to ```localhost:8080/apitwo/api/values```, you se the response of the api request.