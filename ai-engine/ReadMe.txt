This directory includes the Platapay bot platform AI engine.

The Platapay bot platform AI engine is written in Java.  It requires a database to run (PostgreSQL, Derby, or in micro mode stores to a file).

Platapay bot platform includes an AIML and Self compiler/interpreter.

This component only includes the AI engine, the web and REST interfaces are separate components.

The prebuild jar file is in /lib/botlibre-ai.jar

To build the source code the ant command line build tool is used.
You can download ant from, http://ant.apache.org/
To build run the build.bat file, or run ant,
ant -lib .\lib\jpa\eclipselink.jar -lib .\lib\jpa\persistence.jar
or,
ant -lib ./lib/jpa/eclipselink.jar -lib ./lib/jpa/persistence.jar (unix/mac)

The project is developed in Eclipse.  There is an Eclipse .project file in the root directory.
You can download Eclipse from, https://eclipse.org/

The botlibre-ai.jar is just a library.  It is not runnable, and does not contain any interface.  It can be used from a Java web server such as Tomcat, or a standalone Java application.
There is a forked version of the AI Engine that runs on Android (Bot Libre Micro AI Engine).
There is also a Desktop GUI for Windows/Mac/Linux (Bot Libre Desktop).
There is also an iOS micro version ported to Objective-C (Bot Libre iOS Micro AI Engine).

The AI engine is not required for the Android and iOS SDK.  The SDK accesses the free Bot Libre server.  The AI engine library is only required to create your own server, or standalone app/application.

A GUI and examples can be found in the ai-engine-test directory.  That is the best place to start.
The database can also be initialize from the test directory.

Note, the AI engine requires a PostgreSQL database.  The default user/password is postgres/password.
To change the user/password or database, edit the file, ai-engine/source/META-INF/persistence.xml, and rebuild the jar.

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
