## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!(Project 13 Network Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  -install-elk.yml
  - dvwa-playbook.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml

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
- A loadbalancer is used to serve as a point of access for service that is served by multiple machines. 
- A jump box is used as a gateway to gain entry into a remote network.  Most of the time the primary access is through ssh.  Without a key the access is forbidden.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system resources.
- Filebeat is used to watch system logs and forward any changes to the Elasticsearch Host.
- Metricbeat is used for gathering metrics and system resources usage to display in Elasticsearch.

The configuration details of each machine may be found below.

| Name     | Function            | IP Address | Operating System |
|----------|---------------------|------------|------------------|
| Jump Box | Gateway             | 10.0.0.4   | Linux            |
| Web1     | Web Server          | 10.0.0.5   | Linux            |
| Web2     | Web Server          | 10.0.0.6   | Linux            |
| ELK      | ElasticSearch Stack | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.241.129.108

Machines within the network can only be accessed by jumpbox.
- Jumpbox
  - PublicIP: 20.94.226.169
  - PrivateIP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible  | Allowed IP Addresses |
|----------|----------------------|----------------------|
| Jump Box | SSH -Yes             | 73.241.129.108       |
| WEB1     | SSH from Jumpbox -No | 52.247.239.28 -WebLB |
| WEB2     | SSH from Jumpbox -No | 52.247.239.28 -WebLB |
| WEBLB    | HTTP-80 -Yes         | *                    |
| ELK      | Kibana-5601 -Yes     | *                    |
| ELK      | HTTP API-9200 -Yes   | *                    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating configuration with Ansible is that it allows for full automation of a specific server and reduces configuration errors.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install Docker: Installs the docker code to the remote server
- Install Python3_pip:  Allows for additional docker modules to be installed easier.
- Docker Module: Command that installs the necessary docker component modules.
- Max Memory: Allows the server to launch by increasing memory.
- Download and Launch Elk Container: Downloads the ELK docker container and initializes it with the ports.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(docker-ps-output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.4
- 10.0.0.5
- 10.0.0.6
- 10.1.0.4

We have installed the following Beats on these machines:
- We have installed Filebeat and Metricbeat on Web1, Web2, and ELK machines.

These Beats allow us to collect the following information from each machine:
- Filebeats collect system type events like logins to see who is active on the system.
- Metricbeats collects cpu usage and memory to see what programs are taking system resources.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible/roles.
- Update the hosts file to include ELK ip.
- Run the playbook, and navigate to http://20.114.223.225:5601/app/kibana to check that the installation worked as expected.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._