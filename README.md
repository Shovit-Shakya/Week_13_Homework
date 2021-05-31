# Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img width="831" alt="Network config" src="https://user-images.githubusercontent.com/84818429/120159617-c096d680-c238-11eb-8557-65152450b095.PNG">


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible playbook and config file may be used to install only certain pieces of it, such as Filebeat.

- Ansible/docker-python-install.yml
- Ansible/hosts.txt
- Ansible/ansible_config.txt
- Ansible/install-ELK.yml
- Ansible/filebeat-playbook.yml
- Ansible/filebeat-config.txt
- Ansible/metricbeat-playbook.yml
- Ansible/metricbeat-config.txt

  

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting restricting to the network.
- What aspect of security do load balancers protect?
  * A load balancer intelligently distributes traffic, also adds additional layers of security to your system without any changes to your application. LB also protects the system from DDoS attacks by shifting attack traffic.
  
- what is the advantage of a jump box?
  * The advantage of a jump box is to give access to the user from a single node that can be secured and monitored. The use of a jump box guarantees a single, secure, point of entry to network resources.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file and system statistics.
- What does Filebeat watch for?
  * Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.Filebeat watches for any information in the file system which has been changed and when it has.
  
- What does Metricbeat record?
  * Metricbeat takes the metrics and statistics that collects and ships them to the output you specify, such as Elastisearch or logstash
 
The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web -1   | Webserver| 10.0.0.5   | Linux            |
| Web -2   | Webserver| 10.0.0.6   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- [Public IP address] e.g [49.199.30.98]

Machines within the network can only be accessed by Jumpbox VM
- The Jump box VM has access to web-1 and web-2 and its ip address is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses     |
|----------|---------------------|--------------------------|
| Jump Box | SSH-22              | 49.199.30.98             |
| web-1    | No                  | 13.73.102.223, 10.0.0.4  |
| web-2    | No                  | 13.73.102.223, 10.0.0.4  |
| ELK-VM   | TCP 5601/9200       | 10.1.0.4                 |
|LB        | Http 80             |[Personal IP]             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The primary benefit of Ansible is it allows IT administrators to automate daily tasks. So that we can focus on more productive tasks.

The playbook implements the following tasks:
- Install Docker
- Install python3-pip
- Install docker python module
- Download and launch a docker elk container


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1, 10.0.0.5
- Web-2, 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat allows to collect log events from host.
- Metricbeat allows us to collect metrics and statistic from host

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat.cfg file to /etc/ansible/filebeat-config.yml.
- Update the filebeat-config.yml file to include
- https://github.com/Shovit-Shakya/Week_13_Homework/blob/main/Ansible/filebeat-playbook.yml
- Run the playbook, and navigate to check the installation

Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it?
  * filebeat-playbook.yml is copied to /etc/filebeat/filebeat.yml 
- Which file do you update to make Ansible run the playbook on a specific machine?
- https://github.com/Shovit-Shakya/Week_13_Homework/blob/main/Ansible/hosts.txt
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- edit the /etc/ansible/host file to add webserver/elkserver ip addresses
- Which URL do you navigate to in order to check that the ELK server is running?
-    www.publicip:5601 (Kibana) [20.36.46.94:5601]
