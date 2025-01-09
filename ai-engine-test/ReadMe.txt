This is the test component for the Platapay bot platform.

This directory contains several test classes written in JUnit in Java.

The prebuild jar file is in /lib/botlibre-ai-test.jar

To build the source code the ant command line build tool is used.
You can download ant from, http://ant.apache.org/
To build run ant, or the build.bat file.

The project is developed in Eclipse.  There is an Eclipse .project file in the root directory.
You can download Eclipse from, https://eclipse.org/

This component also includes a standalone GUI that can be used for testing or to create and access a bot instance.
To run the GUI run "ant gui" or the gui.bat file.

The AI engine requires a PostgreSQL database.  The default user/password is postgres/password.
To change the user/password or database, edit the file, ai-engine/source/META-INF/persistence.xml.
You will need to rebuild the botlibre-ai.jar and copy it to the ai-engine-test lib directory.

To create and initialize the database run "ant initdb" or the initdb.bat file.

The Twitter, Facebook, and Freebase support also require developers keys from Twitter, Facebook, and Google.

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
