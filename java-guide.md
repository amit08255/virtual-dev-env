# Java Dev Guide

## Setup Maven Build Tool Linux

* Download Maven from: https://maven.apache.org/download.cgi

* Extract Maven compressed file. Rename Maven folder to maven and move folder to /bin directory using command:

  ```sh
  sudo mv maven /bin
  ```

* Then use below command to create shortcut of maven binary to create an executable command:

  ```sh
  sudo ln -s /bin/maven/bin/mvn /bin/mvn
  ```

* Execute Maven using command: `mvn`

## Setup Spring Project

* Go to: https://start.spring.io/ to create demo setup Spring project using Spring intializer.

* Extract project files. Open terminal in project directory and use below command to compile:

  ```sh
  mvn compile
  ```
  
* When compilation is finished, you should find the compiled .class files in the target/classes directory.

* To create JAR package of your Spring project use below command:

  ```sh
  mvn package
  ```

* To execute the JAR package use command:

  ```sh
  java -jar target/filename.jar
  ```

