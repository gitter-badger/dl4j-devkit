# dl4j-devkit

[![Join the chat at https://gitter.im/deeplearning4j/dl4j-devkit](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/deeplearning4j/dl4j-devkit?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
- the "devkit", a reference build environment for nd4j & deeplearning4j

## Contents
- OpenJDK 8
- Maven 3.3
- gcc
- blas

## Using
The devkit provides an interactive shell to build nd4j and deeplearning4j.   The shell is packaged as a docker image. 

### Install prerequisites
Mac OSX:
1. Install boot2docker:
```
brew install boot2docker
```
2. Install docker-compose:
```
pip install docker-compose
```

### Author a docker-compose file
To simplify launching the shell, author a docker-compose file into your workspace directory.   Your workspace directory should contain the nd4j, deeplearning4j, and other such repositories.

Write to `./docker-compose.yml` the following snippet:
```
shell:
  image: deeplearning4j/dl4j-devkit:latest
  volumes:
    - .:/workspace
    - $HOME/.m2:/home/vagrant/.m2
  working_dir: /workspace  
  environment:
    - CONTAINER_NAME=shell
  command: bash
```

### Start the shell 
```
$ docker-compose run --rm shell
```
A bash shell starts up into the workspace directory that is shared into the container at `/workspace`.
```
[vagrant@abd582a75122#shell workspace]$ pwd
/workspace
[vagrant@abd582a75122#shell workspace]$ ls
Canova  deeplearning4j  dl4j-spark-ml nd4j
```
Build projects at will:
```
[vagrant@abd582a75122#shell workspace]$ cd nd4j
[vagrant@abd582a75122#shell nd4j]$ mvn install -DskipTests
...
[INFO] BUILD SUCCESS
...
[vagrant@abd582a75122#shell nd4j]$
```
Exit the shell when finished:
```
[vagrant@abd582a75122#shell workspace]$ exit
```
