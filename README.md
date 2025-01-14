# Lippia Web project

# Purpose
This project has the intention of showing you a web automation testing suite case, using Lippia Automation Framework by using Gherkin and Page-Object Model pattern.
This project includes the required components and configuration files to simply download and run the set of tests in your local computer.

## System Requirements: 
+ jdk: https://docs.oracle.com/en/java/javase/index.html 
+ maven: https://maven.apache.org/download.cgi 
+ git client: https://www.atlassian.com/git/tutorials/install-git 


# Getting started


- # Running with Maven

  + ### First Step

    + Download and unzip the source repository for this guide, or clone it using Git:   
    ```
    $ git clone https://github.com/martinchogimenez/testing_automation_with_lippia_framework_WEB.git
    ```

    + Go to root directory:   
    ```
    $ cd testing_automation_with_lippia_framework_WEB
    ```   

  + ### Second Step

    If you want to run tests locally, you need maven as a minimum requirement   
    + Make sure you have installed maven correctly   

    ```
    $ mvn --version

      OUTPUT:
        Apache Maven 3.8.2 (ea98e05a04480131370aa0c110b8c54cf726c06f)
        Maven home: /opt/apache-maven-3.8.2
        Java version: 13.0.5.1, vendor: Debian, runtime: /usr/lib/jvm/java-13-openjdk-amd64
        Default locale: en_US, platform encoding: UTF-8
        OS name: "linux", version: "5.10.0-6parrot1-amd64", arch: "amd64", family: "unix"
    ```

    If you don't see a similar output:
    + Make sure you have the maven path configured   
    #### Linux user
    ```
    $ grep -Ew '(.*)(M2_HOME)' ~/.bashrc

      OUTPUT:
        M2_HOME=/opt/apache-maven-3.8.2
        PATH=$PATH:$M2_HOME/bin
    ```   
    #### Windows user
    ```
    $ set

      OUTPUT:
        M2_HOME=C:\Program Files\apache-maven-3.8.2
        PATH=%PATH%;%M2_HOME%\bin;
    ```

  + ### Third Step

    + To run the tests with maven, we must execute the following command:   

    ```
    $ mvn clean test
    ```


### Reports are generated in the folder called **target**, which will be generated once the execution of the test suite is finished.   

```
├── testing_automation_with_lippia_framework_WEB
|   ├── docs
|   |   └── ...
|   ├── src
|   |   └── ...
│   ├── target
│   |   └── reports
|   |       └── index.html
|   └── ...
```

Folder's description:

|Path   |Description     |
|-------|----------------|
|main\java\\...\contants\\\*.java|Folder with all the **web elements' locators** matching steps with java code|
|main\java\\...\services\\\*.java|Folder with all the **PageObjects** matching steps with java code|
|main\java\\...\steps\\\*Steps.java|Folder with all the **steps** which match with Gherkin Test Scenarios |
|test\resources\web.features\\\*.feature|Folder with all the **feature files** containing **Test Scenarios** and **Sample Data** |
|main\resources|Folder with all configuration needed to run Lippia |

The **steps** are defined to execute the *Test Scenarios* defined in Gherkin language.

## Runners
***
```
├── testing_automation_with_lippia_framework_WEB
│   ├── docs
│   │   └── ...
│   ├── src
│   │   ├── main
│   ├── java
│   │     └── ...
│   ├── resources 
│   │     └── ...
│   ├── test
│   │     ├── resources
│   │     │ └── ...
│   │ 
│   ├── pom.xml
│   ├── testngParallel.xml
│   ├── testngSecuencial.xml
│          
│  
```


The test cases are executed using **TestNG** class. This class is the main entry point for running tests in the TestNG framework. By creating their own TestNG object and invoke it on a testng.xml.

|**Attribute** | **Description** | 
|--------------|-----------------| 
|name   | The name of this suite. It is a **mandatory** attribute. |  
|verbose   | Whether TestNG should run different threads to run this suite. |  
|parallel   | Whether TestNG should run different threads to run this suite. |
|thread-count   | The number of threads to use, if parallel mode is enabled (ignored other-wise). |  
|annotations   | The type of annotations you are using in your tests. |  
|time-out   | The default timeout that will be used on all the test methods found in this test. |  

### testngSecuencial.xml  

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<suite name="BDD Test Suite" verbose="10" parallel="tests" thread-count="1" configfailurepolicy="continue">
    <test name="TestNg Secuencial runner Tests" annotations="JDK" preserve-order="true">
        <classes>
            <class name="com.crowdar.bdd.cukes.TestNGSecuencialRunner"/>
        </classes>
    </test>
</suite>

```

### testngParallel.xml  

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<suite name="BDD Test Suite" verbose="1" parallel="methods" data-provider-thread-count="1" thread-count="1" configfailurepolicy="continue">
    <test name="TestNg parellel runner Tests" annotations="JDK" preserve-order="true">
        <classes>
            <class name="com.crowdar.bdd.cukes.TestNGParallelRunner"/>
        </classes>
    </test>
</suite>
```


### How to select Sequential or Parallel Runner:
 
**Sequential Runner:**  
    
- In the pom.xml file, it looks for the POM in the current directory and assign the value of "testngSecuencial.xml".  
    
- This would be as follows:
```  
        <runner>testngSecuencial.xml</runner>
```         

**Parallel Runner:**  
    
- In the pom.xml file, it looks for the POM in the current directory and assign the value of "testingParalel.xml"  
    
- This would be as follows:  
```
        <runner>testngParallel.xml</runner>
```        
