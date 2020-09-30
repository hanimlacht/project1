# George Nava Project 1
# UCSD Cybersecurity Bootcamp
# Within Azure create a VNET of VMs for Ansible, Docker, DVWA, and ELK
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![project1\Diagrams_project1.jpg](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.


  - ![install-elk.yml](project1/ansible/install-elk.yml)
  - ![install-filebeat.yml](project1/ansible/filebeat-playbook.yml)
  - ![install-metricbeat.yml](project1/ansible/metricbeat-playbook)

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

What aspect of security do load balancers protect?
Load balancers increase the availability of the Back End Pool by performing a health probe of each individual server thus determining their availability

What is the advantage of a jump box?
Jump Box servers access and manage devices in the security zone.  A Jump Box provides internal access to web servers.  A Jump Box is also hosts an open source software provisioning, configuaration management, and application deployment tool called Ansible.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
What does Filebeat watch for?
Filebeat collects and parses logs created by the system logging service

What does Metricbeat record?
Metricbeat monitors the metrics from the Docker server
diskio,cpu,healthcheck, info, memory, and network

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.2.0.4   | Linux            |
| web-1    | DVWA     | 10.2.0.5   | Linux            |
| web-2    | DVWA     | 10.2.0.6   | Linux            |
| web-3    | DVWA     | 10.2.0.7   | Linux            |
| ELK-VM   | ELK      | 10.3.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Local IP and internal 10.2.0.4

Machines within the network can only be accessed by the Jump-Box-Provisioner 10.2.0.4


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Local IP             |
| web-1    | No                  | 10.2.0.4             |
| web-2    | No                  | 10.2.0.4             |
| web-3    | No                  | 10.2.0.4             |
| ELK-VM   | Yes                 | Local IP             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the configuration management is automated in Ansible.  The advantage is that repetitive tasks are accomplished using standardized playbooks.


The Ansible playbook implements the following tasks:

- Install docker.io
- Install Python
- Increase virtual memory
- Install docker module
- Download and launch and ELK docker container
- Enable the docker service to start on boot



The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(project1/Diagrams/.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- web-1 10.2.0.5
- web-2 10.2.0.6
- web-3 10.2.0.7

We have installed the following Beats on these machines:
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat monitors log files and collects log events then forwards them to either Logstash or Elasticsearch for indexing. It can collect SSH login attempts.

Metricbeat collects metrics and statistics from the OS and services running on the server and sends them to either Logstash or Elasticsearch.  It can capture Docker metrics which reveal the health and status of the Docker containers.  


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the filebeat-configuration.yml file to _/etc/ansible/files.
- Update the filebeat-configuration.yml file to include the ELK-Sever IP 10.3.0.4
- Run the filebeat-playbook, and navigate to Kibana to check that the installation worked as expected.

- Copy the metricbeat-configuration.yml file to _/etc/ansible/files.
- Update the metricbeat-configuration.yml file to include the ELK-Sever IP 10.3.0.4
- Run the metricbeat-playbook, and navigate to Kibana to check that the installation worked as expected.

