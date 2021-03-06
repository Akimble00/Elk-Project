## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[![](https://github.com/Akimble00/Elk-Project/blob/main/Diagram/Diagram.png)](https://github.com/Akimble00/Elk-Project/blob/main/Diagram/Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ 
   filebeat-plabook.yml
This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly PROTECTED, in addition to restricting TRAFFIC to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?
 Layer 4 of the OSI model. Load balancers prevent servers from breaking down from being overloaded. 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs system traffic.
- _TODO: What does Filebeat watch for?
 Filebeat watches the log files and collects data
- _TODO: What does Metricbeat record?
 Metricbeat records machine metrics and stats such as uptime, CPU and RAM usage,

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.4   | Linux            |
| Elk Stack| Monitoring | 10.2.0.4   | Linux            |
| Web-1    | Server     | 10.0.0.5   | Linux            |
| Web-2    | Server     | 10.0.0.5   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Bo-x machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
10.0.0.4

Machines within the network can only be accessed by ____.
Jump-Box VM 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses   |
|-----------|---------------------|------------------------|
| Jump Box  | Yes                 | 20.127.39.89/10.0.0.4  |
| Web-1     | No                  | 10.0.0.5               |
| Web-2     | No                  | 10.0.0.6               |
| Elk-Stack | No                  | 10.2.0.4               |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible? 
- Ansibles can be used to automate daily tasks so IT administrators can save time and perform tasks more efficiently resulting >
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
-.install docker.io
-.install pip3
-.install docker python module
-.increase virtual memory
-.download and launch docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[![](https://github.com/Akimble00/Elk-Project/blob/main/Images/docker_ps_output.png)](https://github.com/Akimble00/Elk-Project/blob/main/Images/docker_ps_output.png)
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

| Name      |           | IP Addresses   |
|-----------|-----|-----------------|
| Web-1     |           | 10.0.0.5       |
| Web-2     |           | 10.0.0.6       |

We have installed the following Beats on these machines:
-.filebeat
-.metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat collects log files from specific locations. Metricbeat records the statistics and provides charts from the OS as well as services running on the server,the amount of RAM or CPU usage being used on the webservers at given time can be seen.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the Playbook file to Ansible.
- Update the host file to include webserver and ELK
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it? 
filebeat-playbook.yml will be copied to the /etc/ansible/host/
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
filebeat.yml has to be updated
 which is a configuration file that will be dropped into the Elk-Server during the run of the ansible-playbook.
update the host.cfg file in the ansible directory 
you will need to create a new group called [elkservers] and add the Private IP of the Elk-Server to the group. 
designate the Private IP of the Elk-Server in lines 1106 and 1806.

- _Which URL do you navigate to in order to check that the ELK server is running? 
http://publicIP/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

ssh azureuser@ 20.118.203.38(JumpBox)
sudo docker container list -a 
sudo docker start epic_shamir (name of the container)
sudo docker attach epic_shamir (name of the container)
cd /etc/ansible/
ansible-playbook elk.yml (configures Elk-Server and starts the Elk container on the Elk-Server) wait a couple minutes for the implementation of the Elk-Server
cd /etc/ansible/roles/
ansible-playbook filebeat-playbook.yml (installs Filebeat and Metricbeat)
open a new web browser (Elk-Server PublicIP:5601) which leads to Kibana
