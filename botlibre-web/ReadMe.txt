This directory includes the Platapay bot platform Web Platform.

The Platapay bot platform Web Platform is written in Java.  It requires a Java web server (Tomcat) and a database (PostgreSQL) to run.

The prebuild war file is in /web/platapaybot.war

To build the source code the ant command line build tool is used.
You can download ant from, http://ant.apache.org/
To build run the build.bat file, or run ant,
ant -lib .\lib\jpa\eclipselink.jar -lib .\lib\jpa\persistence.jar war
or on Linux/Mac,
ant -lib ./lib/jpa/eclipselink.jar -lib ./lib/jpa/persistence.jar war

The project is developed in Eclipse.  There is an Eclipse .project file in the root directory.
You can download Eclipse from, https://eclipse.org/

Refer to /doc/Platapay-Web-Installation-Guide.pdf for installation.

The Twitter, Facebook, Skype, Kik, WeChat, and Google support also require developers keys from Twitter, Facebook, Microsoft, Kik, WeChat, and Google.

## Installation Guide for Ubuntu

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
