# End to End DevSecOps Project for DevOps Engineers

![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709575574725/94d5111a-0cbb-4cdb-90d1-0ab973deeffb.webp?w=1600&h=840&fit=crop&crop=entropy&auto=compress,format&format=webp)

### In this project, we will learn about  DevOps and DevSecOps tools in one project:

### Tools Covered:
-  Linux
-  Git and GitHub
-  Docker
-  Docker-compose
-  Jenkins CI/CD
-  SonarQube
-  OWASP
-  Trivy 

#

## Pre-requisites to implement this project:

-  AWS EC2 instance (Ubuntu) with instance type t2.large and root volume 29GB.

-  Jenkins installed <br>
    - Reference: <b><a href="https://www.jenkins.io/doc/book/installing/linux/#long-term-support-release"><u> Jenkins installation </a></u></b>

-  Docker and docker-compose installled
```bash
    sudo apt-get update
    sudo apt-get install docker.io -y
    sudo apt-get install docker-compose -y
```

- Trivy installed <br>
    - Reference: <b> <a href="https://github.com/DevMadhup/Trivy_Installation_and_implementation/blob/main/README.md"><u>Trivy Installation</a></u></b>

- SonarQube Server installed
```bash
    docker run -itd --name sonarqube-server -p 9000:9000 sonarqube:lts-community
```
#
## Steps for Jenkins CI/CD:

1)  Access Jenkins UI and setup Jenkins

![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709492443443/a929feef-80f0-4ac6-857e-5c42aa797500.png)

#

2)  Plugins Installation:

    - Go to <b><i><u>Manage Jenkins</u></i></b>, click on <b><i><u>Plugins</u></i></b> and install all the plugins listed below, we will require for other tools integration:

        - SonarQube Scanner (Version2.16.1)
        - Sonar Quality Gates (Version1.3.1)
        - OWASP Dependency-Check (Version5.4.3)
        - Docker (Version1.5)
#

3) Go to SonarQube Server and create token

    - Click on <b><i><u> Administration </u></i></b> tab, then <b><i><u> Security </u></i></b>, then <b><i><u> Users </u></i></b> and create Token.
    -  Create a webhook to notify Jenkins that Quality gates scanning is done. (We will need this step later)

        - Go to SonarQube Server, then <b><i><u> Administration </u></i></b>, then <b><i><u> Configuration </u></i></b> and click on <b><i><u> Webhook </u></i></b>, add webhook in below <b>Format</b>:
        > http://<jenkins_url>:8080/sonarqube-webhook/
        
        Example: 
        
        ```bash
            http://34.207.58.19:8080/sonarqube-webhook/
        ```

        ![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709569154485/e40c2233-7124-4540-8c65-7eefafeba5c7.png)


        ![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709569229459/e0a7822b-12d4-49cc-bafa-c3651d707f13.png)

#

4) Go to Jenkins UI <b><i><u> Manage Jenkins </u></i></b>, then <b><i><u> Credentials </u></i></b> and add SonarQube Credentials.

![image](![image](https://github.com/Akashdhengale/node-todo-cicd/assets/145600867/7c1582f7-fed7-4853-95e1-4e78e47bf632)

#

5) Now, It's time to integrate SonarQube Server with Jenkins, go to <b><i><u> Manage Jenkins </u></i></b>, then <b><i><u> System </u></i></b> and look for <b><i><u> SonarQube Servers </u></i></b> and add SonarQube.

![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709568464904/d0bebc90-f459-4b8d-8963-7ab5bbccb7a0.png)

#

6) Go to <b><i><u> Manage Jenkins </u></i></b>, then <b><i><u> tools </u></i></b>, look for <b><i><u> SonarQube Scanner installations </u></i></b> and add SonarQube Scanner.

> Note: Add name as ```Sonar```

![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709568701080/8466bdd9-0c0e-4c7b-bbe8-317f5543ad54.png)

7) Integrate OWASP with Jenkins, go to <b><i><u> Manage Jenkins </u></i></b>, then <b><i> tools </i></b>, look for <b><i><u>Dependency-Check installations</u></i></b> and add Dependency-Check.

> Note: Add name as ```dc```

![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709568823781/ff27b469-7a14-4907-87db-34a33ab87a9d.png)

#

8) For trivy, we have already installed it, in pre-reuisites.

![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709568982133/8d8afee9-59ba-4103-8e29-87dfe5c5f734.png)

#

9) Now, It's time to create a CI/CD pipeline in Jenkins:
    -  Click on <b><i><u>New Item</u></i></b> and give it a name and select <b><i><u>Pipeline</u></i></b>.
    -  Select <b><i><u>GitHub Project</u></i></b> and paste your GitHub repository link.
    -  Scroll down and in <b><i><u>Pipeline</u></i></b> section select <b><i><u>Pipeline script from SCM</u></i></b>, because our Jenkinsfile is present on GitHub.

    ![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709569389847/84d0b6dd-8a70-4c91-91c7-8b013ad09dc6.png?auto=compress,format&format=webp)

    ![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709569512657/eaded27d-7543-4100-ba9d-77254f05876b.png?auto=compress,format&format=webp)

    ![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709569560080/201ea968-9568-4e90-ae7a-fd75a39a80b6.png?auto=compress,format&format=webp)

   
#

10) At last run the pipeline and after sometime your code is deployed using DevSecOps.

![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709567925365/c27c9cd6-05e3-4dbb-a7bd-82ed652b0754.png)

![image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709569731072/18dd3452-05a3-4f64-b273-83e461d2b01a.png?auto=compress,format&format=webp)
#

<b>Congratulations!!! You have done it</b>

- If you find any issue during the execution of this project, let me know on LinkedIn

- Happy Learning :)


### ##### For further insights, please visit my Hashnode blog: [Link to my Hashnode blog](https://radhe123.hashnode.dev/project-building-a-comprehensive-devsecops-cicd-pipeline-for-nodejs-todo-application)

