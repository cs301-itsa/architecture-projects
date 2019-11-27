# Project - App

For architecture wise, the app requires the following services from AWS as a prerequisite

## Overview of our solution
![Solution View](./images/solution-view.png)

*Take note that OPTIONAL are things we did but are not necessary for the app itself*

- RDS Aurora DB
This is a relational DB used to store the data of the loans and transactions
Create a new instance of the DB engine, in this setup we are using AWS RDS Aurora DB
Once setup, import the db schema from app/Database Schema SQL/MinimoniesDatabases.sql
Take note of the DB endpoints
[OPTIONAL] Read Replica

- API Gateway
Start a new API gateway from AWS
app/API Schema/Export as Swagger.json -> import this schema to build the gateway 
need to change individual main endpoints to the microservice instance or LB
[OPTIONAL] Custom Domain, ACM Cert as Edge Optimised

- DynamoDB
This is a non relational DB to help store the session data via the AWS PHP SDK
Create a new table called "sessions"

- SQS
Create a queue called "Minimonies", take note of the ARN


This folder contains mainly 2 folders that are required to get the base of the app running.

- App
Inside this folder is the root to the codes to the webapp. It can be deployed to any server running Apache + PHP 7.2 or above.
app\App\include\common.php-> Need to update the API key to reflect the new API key to power DynamoDB
app\App\include\dynamo_session_handler.php -> need to change the URL to reflect on the address of where the microservices are deployed to

- Microservices
Inside this folder contains multiple folder which are the root to the microservices codes that are required to power the webapp. It can be deployed to any server running Apache + PHP 7.2 or above.

The following files are the location where you need to update the Access Keys and Links
LOANS
app\Microservices\Loans\controller\DatabaseConnector.php -> 

NOTIFICATIONS
app\Microservices\Notifications\config\composer.json
app\Microservices\Notifications\controller\DatabaseConnector.php
app\Microservices\Notifications\src\SESMethods.php
app\Microservices\Notifications\src\SQSMethods.php

TRANSACTIONS
app\Microservices\Transactions\controller\DatabaseConnector.php

USERS
app\Microservices\Users\config\AWSCognitoWrapper.php

