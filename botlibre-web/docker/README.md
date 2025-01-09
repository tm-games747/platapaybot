# About

This folder contains the required Dockerfiles for building the docker container (paphussolutions/botlibre).

A docker-compose file is also included for running the containers. If the required containers are all available online in a Docker registry, then only the docker-compose file is necessary for running the containers.

The containers can be run on any Linux machine with Docker and Docker Compose installed. They can also be used on Mac and Windows machines with Docker installed (where the containers will be run on a virtual machine).

The containers required for the application to work are:
* platapaybot
* postgres:9.4

# How to Build

## platapaybot

Before building the .war file, ensure that the code is correctly configured for deploying as `ROOT.war` (i.e. the URLs in `Site.java` are set to use `localhost` instead of `localhost:8080/platapaybot`, and `SDK.APP` in `sdk.js` is set to `""`).

In addition to these changes, the following changes must be made to `Site.java`: the database host needs to be `"app-db"` instead of `"localhost"`, and the Python server URL needs to be `"http://app-py:6777/"` instead of `"http://localhost:6777/"`.

Perform the Ant build, and save the .war file in the `docker/platapaybot` directory as `ROOT.war`.

To build the platapaybot container using the Dockerfile, run the following command from the platapaybot directory:
\
`$ sudo docker build -it paphussolutions/platapaybot .`

# How to Run

Before running, ensure that Docker and Docker Compose are working.

To start the containers using Docker Compose, run the following command from the same directory as the `docker-compose.yml` file:
\
`$ sudo docker-compose up`

# Step-by-Step Guide for Installing `platapaybot` on Ubuntu

To install `platapaybot` on Ubuntu, follow these steps:

* Update your package list and install necessary packages:
  ```sh
  sudo apt update
  sudo apt install openjdk-11-jdk ant postgresql
  ```

* Clone the repository:
  ```sh
  git clone https://github.com/tm-games747/platapaybot.git
  cd platapaybot
  ```

* Set up the PostgreSQL database:
  * Start the PostgreSQL service:
    ```sh
    sudo service postgresql start
    ```
  * Switch to the PostgreSQL user:
    ```sh
    sudo -i -u postgres
    ```
  * Create a new database and user:
    ```sh
    psql
    CREATE DATABASE platapaybot;
    CREATE USER platapaybotuser WITH ENCRYPTED PASSWORD 'password';
    GRANT ALL PRIVILEGES ON DATABASE platapaybot TO platapaybotuser;
    \q
    exit
    ```

* Update the database configuration in `ai-engine/source/META-INF/persistence.xml` to match the new database settings.

* Build the project using Ant:
  ```sh
  cd ai-engine
  ant -lib ./lib/jpa/eclipselink.jar -lib ./lib/jpa/persistence.jar
  cd ../ai-engine-test
  ant -lib ../ai-engine/lib/jpa/eclipselink.jar -lib ../ai-engine/lib/jpa/persistence.jar
  ```

* Initialize the database:
  ```sh
  ant initdb
  ```

* Run the GUI for testing:
  ```sh
  ant gui
  ```

This will set up and run the `platapaybot` on your Ubuntu system. For more details, refer to the `ai-engine/ReadMe.txt` and `ai-engine-test/ReadMe.txt` files.
