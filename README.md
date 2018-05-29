SpringBoot - CentOS Docker image
========================================

All of that is sampled from [Wildfly openshift s2i project](https://github.com/openshift-s2i/s2i-wildfly)

Supported tags and respective `Dockerfile` links for image [s2i-spring](https://hub.docker.com/r/bespinsbl/s2i-spring/) 
--------------------

* `jdk-8` [(jdk-8)](https://github.com/bespin-sbl/s2i-spring/blob/master/jdk-8/Dockerfile)

This repository contains the source for building various versions of
the Spring Boot application as a reproducible Docker image using
[source-to-image](https://github.com/openshift/source-to-image).
The resulting image can be run using [Docker](http://docker.io).

Versions
--------------------
CentOS versions currently provided are:
* CentOS 7

Java versions currently provided are:
* Openjdk 8

Maven versions currently provided are:
* Maven 3.5

Installation
--------------------
This image is available on DockerHub. To download it, run:

```
$ docker pull bespinsbl/s2i-spring:jdk-$JDK_VERSION
```

for example

```
$ docker pull bespinsbl/s2i-spring:jdk-8 
```

Usage
--------------------
To build a simple `java maven`
using standalone [S2I](https://github.com/openshift/source-to-image) and then run the
resulting image with [Docker](http://docker.io) execute:

```
$ s2i build git://github.com/bespin-sbl/sample-spring bespin-sbl/s2i-spring:jdk-8 sample-spring
$ docker run -p 8080:8080 sample-spring
```

Accessing the application:
```
$ curl 127.0.0.1:8080
```

Repository organization
-----------------------
* `<Java-version>`
    * `Dockerfile`
        CentOS based Dockerfile
    * `s2i/bin/`
        This folder contains scripts that are run by [S2I](https://github.com/openshift/source-to-image):
        * `assemble`
          Build Java Code with Maven.
        * `run`
          Run Spring Boot application server.
    * `contrib/`
        * `setting.xml`
            A setting.xml file.

Image version structure
-----------------------
##### Structure: name/1-2-3
1. Java version - jdk-8

Example: `bespin-sbl/s2i-spring:jdk-8`

Environment variables
---------------------
To set environment variables, you can place them as a key value pair into a `.sti/environment` 
file inside your source code repository or add -e FOO=BAR to `s2i build -e FOO=BAR` .

* MAVEN_ARGS

    Overrides the default arguments passed to maven durin the build process

* MAVEN_ARGS_APPEND

    This value will be appended to either the default maven arguments, or the value of MAVEN_ARGS if MAVEN_ARGS is set.

* JAR_NAME

    Name of the jar file to move into apps directory after maven build `JAR_NAME=*.jar`

* POM_PATH

    Useful for many pom.xml git repositories, specify the path to follow into the repo to find the pom file to use. default to `POM_PATH=.`

* VERSION

    This value will be replace to package version.

Copyright
--------------------
Released under the Apache License 2.0. See the [LICENSE](LICENSE) file.
