# Setup

My recommended way to setup jdk is using the sdk man.
Visit https://sdkman.io/ for more info.
Let’s install sdkman.

## Install SDKMAN

```sh
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

next you type `sdk help`

## Install Java Using SDKMAN

See the list of different java versions available for installation
```sh
sdk list java
```

NOTE: Personally I already have java installed before sdkman. let's sdkman know it
find the full java path
```sh
readlink -f $(which java)
```
Use the path in the below command
```sh
sdk install java 21-local /usr/lib/jvm/java-21-openjdk-amd64
sdk default java 21-local
```


## Install gradle
```sh
sdk install gradle
```

## Create the project
```sh
mkdir practice-java && cd practice-java
gradle init --type java-application --dsl groovy
```
Answer the questions accordingly.

