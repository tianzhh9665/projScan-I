# projScan-I

Author: Tianzhi Huang (th2888)

# Introduction

projScan-I (Project Scan Integrated), aims to construct a multidimensional code based tool in order to help programmers and software developers assess their project’s level of security-related threats and vulnerabilities. projScan-I is implemented to focus on three aspects of them and striving for revealing meaningful information about any security threats and vulnerabilities. These three detecting and scanning aspects are: 1) vulnerabilities caused by code error, misuse of functions, modules, and APIs; 2) vulnerabilities caused by importing and using vulnerable dependencies including those provided Third-Party Libraries; 3) vulnerabilities caused by having duplicate (or high similarity) code snippets (functions, classes, modules) within the same project. projScan-I not only scans the projects, searching for vulnerabilities in these three aspects, but also saves the raw scanning result data, parsing the data of different types of file, and eventually generates a concrete, summarized, and detailed textual report for each of the three detecting aspects. projScan-I is easily deployed and could be run on Linux environment with most of the virtual machine supported, and it is currently supporting scanning projects written in Java and Python.

# What you can find in this repository

- **projScan-I**: contains all the code, scripts, source files, and included jar packages of projScan-I.  
  - Application.java
  - run.sh
  - json-simple-1.1.1.jar
  - jsoup-1.14.3.jar
- **Test Project**: contains the test projects that I used to evaluate the projScan-I project’s performance as well as studying the research questions  
  - CULift
  - Connect4
  - Service-operation
  - Service-client
- **Assignment Related Documentation**: contains all textual assignments files of this final project including: project proposal, revised project proposal, project progress report, project final report, and in-class project demo slides.  
  - COMSE6156_Project_Demo_Tianzhi_Huang.pdf
  - COMSE6156_Project_Progress_Report.pdf
  - COMSE6156_Project_Proposal.pdf
  - COMSE6156_Revised_Project_Proposal.pdf
  - COMSE6156_Project_Report.pdf
- **Generated Reports And Evaluation Results**: contains the reports generated by projScan-I when running against different test projects, three per project. Also it will contains the result generated by the evaluation of research questions.
  - CULift
  - Connect4
  - Service-operation
  - Service-client
  - COMSE6156_Project_Research_Question_Stats.xlsx (experiment result data)
- **Raw Scan Result Data**: contains the raw data generated by the three sub-systems, which projScan-I reads and parses from.
  - CULift
  - Connect4
  - Service-operation
  - Service-client

# Deploy and Run projScan-I

## Linux based Platform

A Linux based platform and virtual machine is required to run projScan-I, the following guidelines and instructions are given based on running projScan-I
on 25GB Ubuntu 18.04.

## Install required software

Run the following command to install Python 3.6 and its environment:
```
sudo apt-get update
sudo apt-get install git python-virtualenv python-dev
sudo apt-get install python3-pip

python3 --version // check what version of python3 are currently being used
sudo apt-get install python3.6
```

Run the following command or refer to the [Docker documentation](https://docs.docker.com/engine/install/ubuntu/) to install Docker:
```
sudo apt-get update
sudo apt-get install \
   ca-certificates \
   curl \
   gnupg \
   lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

sudo docker run hello-world // verify the Docker engine is installed correctly
```

Run the following command to install Java JDK and JRE:
```
sudo apt update
Java --version // check if Java is already installed

sudo apt install openjdk-11-jdk
sudo apt install openjdk-11-jre
```

Run the following command to install copydetect:
```
pip install copydetect
```

## Running projScan-I

1. Before start running projScan-I, generate a [Github Token](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) with **read:packages** scope.  

2. Set an environment variable **GITHUB_TOKEN** on the virtual machine by running:
```
export GITHUB_TOKEN=<Github Token generated>
```  
3. Clone the **projScan-I** folder to your virtual machine.
4. Place **Application.java, json-simple-1.1.1.jar, jsoup-1.14.3.jar** inside the project folder which you want projScan-I to scan. **If it is a Java project, make sure you build the project before trying to scan. In this case, place these three files in the same directory as build file (/target)**
5. Place the run.sh in the same directory as your test project.
6. Run the following command to change the execution permission of the script:
```
chmod +x run.sh
``` 
7. Run the run.sh script with two parameters: absolute path to your test project, similarity scanning threshold (float between 0 and 1):
```
// example of running the projScan-I with path as "/home/th2888/cs6156/SANGRIA/service-operation/", and threshold = 0.95

./run.sh /home/th2888/cs6156/SANGRIA/service-operation/ 0.95
``` 
8. projScan-I will run and generate reports in the folder specified in the cell prompt.

## Additional Notes

In cases where any error message occurs during the above process, please install additional packages according to the error messages shown.
