# +++++ JENKINS-MASTER SETUP +++++

#### Install Java  Prerequisite
```
$ sudo su
$ cd
$ sudo apt update
$ hostname
$ hostnamectl set-hostname jenkins-master
$ bash
$ java -version
$ apt-get install openjdk-11-jdk -y
$ java -version
```

<br />


#### Install Jenkins
```
$ wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
$ echo deb https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list
$ sudo apt-get update
$ sudo apt-cache madison jenkins
$ sudo apt-get install jenkins -y                         ## jenkins=2.361.3
$ sudo systemctl start jenkins
$ sudo systemctl enable jenkins
$ sudo systemctl status jenkins
```


<br />


#### Access Jenkins via Browser
```
http://[public_server_ip]:8080
```

<br />


#### Update firewall rules in SG
```
Open Port : 8080
```

<br />


#### Check about jenkins version details
```
http://[public_server_ip]/about/
```


<br />


#### Get Jenkins Administrator password using this command
```
$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<br />


# +++++ JENKINS-SLAVE SETUP +++++

#### Install Java  Prerequisite
```
$ sudo su
$ cd
$ sudo apt update
$ hostname
$ hostnamectl set-hostname jenkins-slave-prod
$ bash
$ java -version
$ apt-get install openjdk-11-jdk -y
$ java -version
```


# +++++ ON JENKINS-MASTER NODE GUI +++++
```
Jenkins Dashboard > Manage Jenkins > Manage nodes and clouds > New node 
                                                                    - Node name
                                                                    - Permanent Agent 
                                                                    - Create



Node
   - Name : slave
   - Description : slave
   - Number of executors : 1
   - Remote root directory : /home/ubuntu
   - Labels : slave
   - Usage : Use this node as much as possible
   - Launch method : Launch agents via SSH
   - Host : 172.31.20.122  (Private_IP_Add)

   - Credentials > Add > 
                       - Domain: default
                       - Kind : SSH Usernme with private key
                                          - Scope : default
                                          - ID : dev-jenkins-slave
                                          - Description : dev-jenkins-slave
                                          - Username : ubuntu
                                          - Private Key > Add > Copy pem file content
                                          - Add                                          
   - Host Key Verification Strategy : Manually trusted key Varification Strategy
   - Availability : Keep this agent online as much as possible
```


## `*************************   EOF   *************************`
