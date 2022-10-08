# Personal Page Config

--- 

## Description

This repository is responsible for the setup and versioning of my web page. From here we can control the values from all the enviromet variables 
and overwrite them if needed. Here we can find docker compose files that will pull the already build image of the server and client and deploy them
in the local machine. Last but not least here we will have the release notes from every release.

## Get a copy up and running

1. If we desire to have a version of the page like its running on ```production``` we only need to find the ```docker-compose.pro.yml``` file and run the following
```shell
docker-compose -p <servername> -f docker-compose.prod.yml up -d
```
