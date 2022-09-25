
# Jenkins

Jenkins is an open-source automation tool written in Java with plugins built for Continuous Integration and Continuous deployment/delivery purposes.
## Install jenkins

* Install Java Development Kit (JDK)
* Set path for the Environmental variable for JDK
* Download and Install Jenkins
* Check if jenkins service is running using (systemctl status jenkins)

## Webhook

Webhook in jenkins triggers pipeline automatically when any changes are done in github repo like commit and push.

* Copy jenkins URL 
* Go to repo settings in github
* Select Add webhook and paste URL
* Append url with /github-webhook/
## Continuous Deployment

Deploy code to production server 
* Go to Jenkins, manage jenkins.
* Install plugin remote ssh
* Connect remote server over ssh
* Configure global property in Jenkins to store the production IP.
* Add credentials, hostname of prod server
* Test connection
Use 
```bash
withCredentials([usernamePassword(credentialsId: 'prodserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) 
```
to connect to production server

## Continuous Deployment using Docker

Push docker image to docker hub

```bash
  withRegistry('https://registry.hub.docker.com', 'docker_hub_login')
```
Ask approval before deploying to production

```bash
  input 'Deploy to Production?'
```
Use milestone to accidently deploying old version over a new version 

```bash
  milestone(1)
```
##Create build agent on a second server 

* Login slave from master using ssh
* Create user's home directory at worker node
* sudo mkdir /var/lib/jenkins
* sudo useradd -d /var/lib/jenkins jenkins
* sudo chown -R jenkins:jenkins /var/lib/jenkins
* sudo mkdir /var/lib/jenkins/.ssh
* Copy the contents of ~/.ssh/id_rsa.pub to the file /var/lib/jenkins/.ssh/authorized_keys
* cat ~/.ssh/id_rsa.pub # Copy the output
* sudo vim /var/lib/jenkins/.ssh/authorized_keys 
* Paste id_rsa contents into jenkins
* Create an .ssh directory on the master in the jenkins directory:
   sudo mkdir /var/lib/jenkins/.ssh
* Copy the known_hosts entry over from the .ssh directory in master   jenkins user's .ssh directory:
  sudo cp ~/.ssh/known_hosts /var/lib/jenkins/.ssh
* Create new node on jenkins master 
* Remote dir:/var/lib/jenkins Labels:Linux Host:Ip of worker node
* Add creds worker node and paste private key

## Monitoring in Jenkins

* Install any monitoring plugins like Prometheus, grafana, datadog   and so on.
* SSH into prometheus server
* Edit vi /etc/prometheus/prometheus.yml file
* Add jenkins target - ip:8080
* Restart prometheus
* Hit endpoints and see data scrape by prometheus


## Backup in Jenkins

* Install Thin Backup plugin
* Create directory jenkinsbackupand cd into it.
* Set write permission to directory
* Go to jenkins enter dir path and backup and restore jenkins.











