# Project Creation

Let's create a project named poc-springboot.
It will reside in `$gp/pocs/poc-springboot`
We will use the spring initializer from vs code.
Press Ctrl-Shift-p
Type: Spring Initializr: Create a maven project

## Project details

1. type: maven
1. language: java
1. version: 21
1. springboot version: 3.5.x
1. groupid: com.lousing
1. artifact id: poc-springboot
1. packagename: com.lousing.poc
1. package type: jar
1. dependencies:
   - Spring Web
   - Spring Data JPA
   - H2 Database

## Making sure we have java 17

Let's isntall sdkman to manage different versions of Java.

**Quick Answer:** Yes, you can install SDKMAN! inside the MSYS2 UCRT64 shell, but you’ll need to ensure that **`zip` and `unzip`** are installed first, along with `curl` and `bash`. These are required for the installation script to work properly.

---

### 🛠 Step-by-Step Guide to Installing SDKMAN! in MSYS2 UCRT64

1. **Open the UCRT64 shell**  
   Launch MSYS2 and select the **UCRT64** environment (you’ll see `ucrt64` in the prompt).

2. **Update MSYS2 packages**

   ```bash
   pacman -Syu
   ```

   Restart the shell if prompted, then run again until everything is up to date.

3. **Install required tools**  
   SDKMAN! needs `zip`, `unzip`, `curl`, and `bash`. Install them with:
   ```bash
   pacman -S zip unzip curl bash
   ```
   (You likely already have `bash` in MSYS2, but installing ensures it’s up to date.)

For me, they got installed in `D:\ProgramData\msys64\usr\bin`
Added this in the path env variable.

4. **Run the SDKMAN! installer**  
    Now open git-bash and use the official installation script:

   ```bash
   curl -s "https://get.sdkman.io" | bash
   ```

5. **Initialize SDKMAN!**  
   After installation, load it into your current shell:

   ```bash
   source "$HOME/.sdkman/bin/sdkman-init.sh"
   ```

6. **Verify installation**

   ```bash
   sdk version
   ```

   You should see the SDKMAN! script and native version numbers.

   ```
    SDKMAN!
    script: 5.20.0
    native: 0.7.14 (windows x86_64)

   ```

7. ** Install Java 17 **
   let's install java 17 and switch to it.
   I am using microsoft as the vendor
   ```bash
   sdk install java 17.0.17-ms
   ```
   Note that sdkman will install packages in `$HOME/.sdkman/candidates/`

---

# Anatomy of a spring boot app

- A spring boot app has a Maven Standard Directory Layout - Established by Maven with 2.0 release in 2005
- project directory
  - pom.xml is a build file containing project metadata like name, version, dependencies
  - readme.md is a file with project info
  - .gitignore file contains info on while files and folder to be ignored by git
  - target/ will contain the build artifacts
  - src/ contains all source code files
    - main/ contains application source files
      - java/ contains source files in java
      - resources/ contains non-java sources files such as property files and images
    - test/ contains test files
      - java/ contains unit test written in java
      - resources/ contains non-java files such as property files or images for unit tests

## Spring boot specific files

1. src/main/resources/application.properties is a property file containing key value pair values that can be used by the springboot app
1. src/main/resources/application.yaml | same as above but in yaml format
1. src/test/resources/application.properties is a file containing key value pairs that can be used for testing
1. src/test/resources/application.yaml is same as above but in yaml format
1. src/main/resources/static is the place you can keep your angular SPA
1. src/main/resources/template is the place to keep web app templates
1. src/main/resources/db/migration is where db migration scripts reside

## Spring boot default classes

1. main class resides in the default package (com.someproject.example)
1. main class is annotated with @SpringbootApplication

> ⚠️ **Warning:**

- Spring boot scans for components in the default and its child packages
- So make sure to keep your components in these places only.

## Referennce

- [Maven Standard Directory layout](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html)
