# Overview

A Docker implementation of MLFlow's Tracking Server.

# Requirements & Components
## Dependencies
Make sure you have the following installed on your machine:
* Docker Desktop
* Docker Compose

## Environment
First things first, you will need to define environment variables. Note that these are the **Server-Side** variables. As such they will populate MLFlow Tracking Server with the information about the backend MySQL Database and the location of a Shared S3 bucket. The client will need to setup environment variables separately.

To set the Server-Side variables, create a .env file with the following environment variables set:

``` bash
MYSQL_DATABASE="..."
MYSQL_USER="..."
MYSQL_PASSWORD=...
MYSQL_ROOT_PASSWORD=...
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
AWS_DEFAULT_REGION="..."
AWS_S3_BUCKET="s3://..."
```

## NGINX Reverse Proxy
This servers to broker incoming connections to the MLFlow Tracking Server.

## MLFlow Tracking Server
The tracking server defaults to listening on the default port supplied by MLFlow, port 5000. This server collects logs and meta data about your experiment and stores them in the MySQL Database. The Tracking Server also provides a web UI which by default is available at:

``` http
http://localhost:5000
```

## MySQL Database
The MLFlow Tracking Server stores incoming logs and metadata about the experiment in this MySQL database.

## AWS S3 Bucket
In order to share Artifacts between the client and server, a shared S3 bucket must be created. Follow the directions on from the [AWS documentation](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/create-bucket.html) to accomplish setting up an S3 bucket.

# Running
Once you have your AWS S3 bucket setup and the environment variables configured correctly, it should be simple to run the server:

``` bash
docker-compose up -d --build
```