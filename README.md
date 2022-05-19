# Project-1
In this repository you can find all the files required for submission for Project 1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

**Note**: The following image link needs to be updated. Replace `diagram_filename.png` with the name of your diagram image file.  

C:\Users\mauri\Downloads\Images\Vnet_Project_1.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

- Load Balancers have the abilitiy to protect the machines in their backend pool from being overloaded by evenly distributing the incoming traffic.
They also ensure redundancy, should one of the servers fail or disconnect. A load balancer also helps mitigate the risk of a DDoS attack.

- The advantage of a Jump Box is that it provides an additional layer of security by giving us a gateway from which to access our virtual network and execute 
administrative tasks without exposing ourselves directly to potential hackers.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network traffic and system logs.
- Filebeat will collect log events and data from the servers on which it is installed.
- Metricbeat will monitor and collect network traffic data from the Operating Systems and services running on the servers.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name               | Function     | IP address | Operating System   |
|--------------------|--------------|------------|--------------------|
| JumpBoxProvisioner | Gateway      | 10.0.0.4   | Linux Ubuntu 18.04 |
| Web-1              | Web server 1 | 10.0.0.5   | Linux Ubuntu 20.04 |
| Web-2              | Web server 2 | 10.0.0.6   | Linux Ubuntu 18.04 |
| Elk                | ELK server   | 10.1.0.4   | Linux Ubuntu 20.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 70.19.95.95

Machines within the network can only be accessed by The Ansible container on the Jump Box Provisioner.
- Jump Box with IP 10.0.0.4 via SSH Port 22

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible     | Allowed IP addresses |
|--------------------|-------------------------|----------------------|
| JumpBoxProvisioner | Yes                     | 70.19.95.95          |
| Web-1              | Yes (Via Load Balancer) | Any                  |
| Web-2              | Yes (Via Load Balancer) | Any                  |
| Elk                | No                      | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
Manual configuration can be time consuming and is more prone to human error. Automated configuration using a provisioner with Ansible allows us to provision a large
number of machines quickly and efficiently. It also ensures that all machines are running identical scripts.

The playbook implements the following tasks:

-Installs docker.io
-Installs python3-pip
-Installs docker python module 
-Increases virtual memory
-Download and run elk container with the correct published ports
-Enables docker service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

"C:\Users\mauri\Downloads\Images\elk.png" 


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web-1 10.0.0.5
- Web-2 10.0.0.6

We have installed the following Beats on these machines:

-Filebeat
-Metricbeat

These Beats allow us to collect the following information from each machine:

-Filebeat collects log data and system logs
-Metricbeat collects network traffic metrics.
 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the config.yml file to etc/ansible/files/
- Update the config.yml file to include the correct IP address under output.elasticsearch and Kibana (and the correct port) of the node you'll provision.
- Run the playbook, and navigate to http://[public IP address of ELK Server]:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
	
	- The file is filebear-playbook.yml copied to /etc/ansible/roles

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
	
	-You would update the hosts file in /etc/ansible. Here you can specify which machines are part of the "webservers" group and should be provisioned with 
	filebeat and metricbeat, and which machine is part of the "elk" group and should be provisioned with the ELK server. 
	Make sure to specify the correct hosts group in the playbook file. 

- _Which URL do you navigate to in order to check that the ELK server is running?
	
	-http://[public IP address of ELK Server]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

ssh -i private_key_file [username]@jump-box-ip-address
sudo docker pull [name of container] to download container
sudo docker run -ti [name of container] bash
sudo docker start [name of container] to start the container
sudo docker attach [name of container] to connect to the Ansible container
Navigate to the /etc/ansible directory
Nano hosts to configure the IP addresses within the "webserver" and "elk" groups
Nano ansible.cfg to specify the remote user.
ansible-playbook [name of playbook] to run the playbook
	
