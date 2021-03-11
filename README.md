## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

ELK-Project/Diagrams/Diagram.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

ELK-Project/Ansible/elk-playbook.yml
ELK-Project/Ansible/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly protected, in addition to restricting traffic to the network.
- Load balancers protect servers from overload and failure, which occurs at layer #4 of the OSI model.
- The advantage of a jump box is that it prevents VM exposure to the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat watches specified log files as well as collects log events and forwards them to Elasticsearch/Logstash.
- Metricbeat records OS and service metrics on the server and sends an output to Elasticsearch/Logstash.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.5   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |
| Web-3    | Server   | 10.0.0.7   | Linux            |
| ELK      |Monitoring| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 5061 Kibana Port

Machines within the network can only be accessed by Jump-Box-Provisioner.
- The only machine allowed to access the ELK VM is the Jump-Box-Provisioner. The IP address of Jump-Box-Provisioner is 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |         Yes         | 13.68.234.66         |
| Web-1    |         No          | 10.0.0.4             |
| Web-2    |         No          | 10.0.0.4             |
| Web-3    |         No          | 10.0.0.4             |
| ELK      |         No          | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because of the efficiency of the process. 

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker Python Module
- Increase Virtual Memory
- Download & Launch Docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

ELK-Project/Images/sebpelk761.JPG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name     |      IP Address     |
|----------|---------------------|
| Web-1    |      10.0.0.5       |
| Web-2    |      10.0.0.6       |
| Web-3    |      10.0.0.7       |

We have installed the following Beats on these machines:
- Filebeat

These Beats allow us to collect the following information from each machine:
- Filebeat: Collects file system data via log events and outputs them for monitoring and analysis.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Playbook file to Ansible.
- Update the host file to include ELK and the webservers.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it?_ The file elk-playbook.yml must be copied into the ansible container within the Jump Box (/etc/ansible).
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
   The file to update to make Ansible run the playbook on a specific machine is the hosts file. To specify which machine(s) to install the ELK server &/or Filebeat on, specify this at the top of the elk-playbook.yml and filebeat-playbook.yml files for "hosts". 
- _Which URL do you navigate to in order to check that the ELK server is running? http://52.251.89.122:5601/app/kibana