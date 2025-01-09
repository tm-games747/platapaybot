# Platapay Bot Platform
An open source platform for artificial intelligence, nlp, chat bots, virtual agents, social media automation, and live chat automation.

* https://www.platapay.com

## Components

* platapay-web : a web platform for developing and hosting bots for the web, mobile, and social media
* ai-engine : artificial intelligence/nlp engine, Java library
* ai-engine-test : JUnit test cases, Java, test GUI
* sdk : Android, iOS, web SDK, (Java, objective C, JavaScript)

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
