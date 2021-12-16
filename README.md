# Microservices-with-Docker
### What is a Microservice?
Microservices are an increasingly popular architecture for building large-scale applications. Rather than using a single, monolithic codebase, applications are broken down into a collection of smaller components called microservices. This approach offers several benefits, including the ability to scale individual microservices, keep the codebase easier to understand and test, and enable the use of different programming languages, databases, and other tools for each microservice.

Docker is an excellent tool for managing and deploying microservices. Each microservice can be further broken down into processes running in separate Docker containers, which can be specified with Dockerfiles and Docker Compose configuration files. Combined with a provisioning tool such as Kubernetes, each microservice can then be easily deployed, scaled, and collaborated on by a developer team. Specifying an environment in this way also makes it easy to link microservices together to form a larger application.

This guide shows how to build and deploy an example microservice using Docker and Docker Compose.

---
> **_NOTE:_**
This guide is written for a non-root user.
---

### Installation
#### [Installing Docker Engine and Docker Compose on Ubuntu](https://www.linode.com/docs/guides/installing-and-using-docker-on-ubuntu-and-debian/)

### Prepare the Environment
* Create a directory for the microservices:
```
mkdir flask-microservices
```
* Create subdirectories for microservices components
```
cd flask-microservices
 mkdir nginx postgres web
 ```
 ### NGINX
* Within the new nginx subdirectory, create a Dockerfile for the NGINX image:
#### **`File: nginx/Dockerfile`**

* Create the nginx.conf referenced in the Dockerfile:
#### **`File: /nginx/nginx.conf`**

### PostgreSQL
* The PostgreSQL image for this microservice will use the official postgresql image on Docker Hub, so no Dockerfile is necessary.
* In the postgres subdirectory, create an init.sql file.
#### **`File: postgres/init.sql`**

### Web
* The web image will hold an example Flask app. Add the following files to the web directory to prepare the app:
* Create a .python-version file to specify the use of Python 3.6.

```python
echo "3.6.0" >> web/.python-version
```
* Create a Dockerfile for the web image.
#### **`File: web/Dockerfile`**

*Create #### **`File: web/app.py`** and add the example app script.

* Add a requirements.txt file with the required Python dependencies:
#### **`File: web/requirements.txt`** 

### Docker Compose
---
> **_NOTE:_**
Docker Compose will be used to be define the connections between containers and their configuration settings.
___
* Create a docker-compose.yml file in the flask-microservice directory.
#### **`File: docker-compose.yml`** 

### Test the Microservices
* Use Docker Compose to build all of the images and start the microservices:
```
cd flask-microservice/ && docker-compose up
```

You should see all of the services start in your terminal.

* Open a new terminal window and make a request to the example application:
```python
curl localhost
```

* Reset the page hit counter:
```
curl localhost/resetcounter
```
