# GitHub-Fundamentals
HW 13 for GW Cyber Security Bootcamp
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/77704521/116789629-c94f8d80-aa7d-11eb-80fb-6741293bd176.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.
	- /etc/ansible/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting acces to the network.
	- Load balancers protect against potential denial-of-service attacks by shifting the attack traffic. The advantage of a jumpbox is that it is a secure and controlled environment to access other VM’s within your network remotely. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the operating system and system services.
	- Filebeat watches for information that has been changed along with when that information was changed in the file system. 
	-  Metricbeat puts the metrics and statistics that is has collected and puts them into the specified location. 

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    | Server   | 10.0.0.8   | Linux            |
| Web-2    | Server   | 10.0.0.9   | Linux            |
| Web-3    | Server   | 10.0.0.7   | Linux            |
| Elk      | Server   | 10.1.0.4   | Linux            |

### Access Policies
The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
	- 71.126.155.137

Machines within the network can only be accessed by SSH through the Jump Box Machine.
	- The machine I allowed to access my ELK VM was the Jump Box VM : 10.0.0.1

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Home IP              |
| Web-1    | No                  | 10.0.0.1             |
| Web-2    | No                  | 10.0.0.1             |
| Web-3    | No                  | 10.0.0.1             |


### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
	- The main advantage of automating configuration with Ansible is that you are able to access commands in multiple servers from one single playbook.

The playbook implements the following tasks:
	- Install: docker.io
	- Install: python3-pip
	- Install: docker
	- Increase virtual memory: sysctl -w vm.max_map_count=262144
	- Launch Elk container: elk


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
	- Web-1: 10.0.0.8
	- Web-2: 10.0.0.9
	- Web-3: 10.0.0.9

We have installed the following Beats on these machines:
	- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
	- Metricbeat collects the metrics and statistics and Filebeat records the changes that are made.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
	- Copy the filebeat.yml file to /etc/ansible/files.
	- Update the filebeat-config.yml file to include the name, private IP address of the ELK server, state, and ports. 
	- Run the filebeat-playbook.yml and navigate to Kibana to check that the installation worked as expected

- Which file is the playbook? Where do you copy it?
	- The file is the filebeat-playbook.yml and it is copied to /etc/ansible/file/filebeat-configuration.yml

- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
	- The file that you update is /etc/ansible/host and you add the IP addresses under the webserver title
- Which URL do you navigate to in order to check that the ELK server is running?
	- www.publicip:5601

-	As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
	- Ssh username@[ip address]
	- docker run -ti container/ansible
	- cd etc/ansible
	- nano hosts [update ip under webservers]
	- nano ansible.config
	- ansible-playbook filebeat_playbook.yml

