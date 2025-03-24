# 2048 Game Deployment on AWS Elastic Beanstalk

This project demonstrates a simple DevOps deployment of the popular 2048 game using Docker, Nginx, and AWS Elastic Beanstalk.

## Project Overview

The project pulls the 2048 game source code from GitHub, sets up an Nginx web server inside a Docker container, and deploys it on AWS Elastic Beanstalk.

## Technologies Used

- **Docker**: Containerizes the application
- **Nginx**: Serves the 2048 game
- **AWS Elastic Beanstalk**: Manages the deployment
- **Ubuntu**: Base OS for the container
- **GitHub**: Hosts the project files

## Deployment Steps

### 1. Clone the Repository
```bash
$ git clone https://github.com/johnUfo/Docker-2048.git
$ cd your-repository
```

### 2. Build the Docker Image
```bash
$ docker build -t 2048-game .
```

### 3. Run the Docker Container
```bash
$ docker run -p 80:80 2048-game
```

### 4. Deploy to AWS Elastic Beanstalk
- Install AWS CLI and Elastic Beanstalk CLI.
- Initialize an Elastic Beanstalk application:
  ```bash
  $ eb init
  ```
- Create and deploy the environment:
  ```bash
  $ eb create 2048-env
  ```

## Dockerfile Explanation

```Dockerfile
FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y nginx zip curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

RUN curl -o /var/www/html/master.zip -L https://codeload.github.com/gabrielecirulli/2048/zip/master && \
    cd /var/www/html/ && \
    unzip master.zip && \
    mv 2048-master/* . && \
    rm -rf 2048-master master.zip

EXPOSE 80

CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf"]
```

## Live Demo

You can access the deployed application at:
[2048 Game on AWS Elastic Beanstalk](http://2048-env.eba-erg3wghn.us-east-1.elasticbeanstalk.com/)
