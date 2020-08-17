## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/amish1983/Project_1/blob/master/Images/Project%20cloud.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the __playook.yml__ file may be used to install only certain pieces of it, such as Filebeat.

- __install-elk.yml__

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load balancers protect from DDoS attacks by distributing traffic evenly between available web servers or denying access when detects unusually high volume of activity. Jump box acts as a controlled gateway to a remote network and used as a bridge between two or more separate DMZ, while also providing security.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Web Servers and system configurations/metrics.
- Filebeat gathers specified log files data and sends it to Elasticsearch or Logstash
- Metricbeat gathers metrics from system and services and sends them to Elasticsearch or Logstash

The configuration details of each machine may be found below.

| Name     | Function       | IP Address | Operating System |
|----------|----------      |------------|------------------|
| Jump Box | Gateway        | 10.0.0.4   | Linux Ubuntu 18.4|
| Web 1    | Web server     | 10.0.0.7   | Linux Ubuntu 18.4|
| Web 2    | Web server     | 10.0.0.7   | Linux Ubuntu 18.4|
| ELK      | Elastic Stack  | 10.1.0.5   | Linux Ubuntu 18.4|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Web Load balancer machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.136.58.128

Machines within the network can only be accessed by Jump Box Provisioner, 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 73.136.58.128        |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| ELK      | No                  | 10.1.0.5, host IP    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- It is not necessary to configure each machine manually, which saves time and resources, also significantly reducing the risk of human error.

The playbook implements the following tasks:
- __name: Install docker.io__ (installs docker container on the machine)
- __name: Install python3-pip__ (installs python programming language translator)
- __name: Install Docker module__ (isntall docker module)
- __Increase virtual memory__ (increases machine's virtual memory to accommodate needs)
- __download and launch a docker elk container__ (launch docker container)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Screenshot of docker ps output] https://github.com/amish1983/Project_1/blob/master/Images/Docker%20ps.jpg

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- __Web-1 10.0.0.7__
- __Web-2 10.0.0.8__

We have installed the following Beats on these machines:
- __Filebeats__
- __Metricbeats__

These Beats allow us to collect the following information from each machine:
Filebeats collects specified log events and sends them to Elasticsearch or Logstash, whereas metricbeats collects system related metrics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __filebeat-configuration.yml__ file to __ansible/_Files__.
- Update the configuration file to include Elk Server Private IP
- Run the playbook, and navigate to __ELK public IP:5601/Kibana__ to check that the installation worked as expected.
- _Which file is the playbook? Where do you copy it? __Filebeat-Playbook.yml__  __etc/filebeat/filebeat.yml__
- _Which file do you update to make Ansible run the playbook on a specific machine? __filebeat-configuration.yml__. 
- _How do I specify which machine to install the ELK server on versus which to install Filebeat on?__By updating host name on the Install-Elk.yml__
- _Which URL do you navigate to in order to check that the ELK server is running? http://52.186.158.66:5601/app/Kibana

_ As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
- ssh azadmin@JumpBoxPublicIP
- ssh-keygen
- curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > filebeat-configuration.yml
- curl https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > metricbeat-config.yml
- sudo su
- Docker start unruffled_ishizaka
- Docker attach unruffled_ishizaka
- nano filebeat-configuration.yml
- nano metricbeat-config.yml
- nano install-elk.yml
- nano filebeat.yml
- nano metricbeat.yml
- ansible-playbook install-elk.yml
- ansible-filebeat-playbook.yml
- ansible-metricbeat-playbook.yml
