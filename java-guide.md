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
