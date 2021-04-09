## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Diagrams/diagram_cloudnetwork.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting  to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system logs and metric data.

The configuration details of each machine may be found below.

| Name      | Function           | IP Address | Operating System |
|-----------|--------------------|------------|------------------|
| RedTeamVM | Gateway (Jump Box) | 10.0.0.4   | Linux            |
| Web-1     | Webserver          | 10.0.0.5   | Linux            |
| Web-2     | Webserver          | 10.0.0.6   | Linux            |
| ElkVM     | Log collector      | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 174.94.30.143/32

Machines within the network can only be accessed by the Jump Box machine (10.0.0.4).

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| RedTeamVM | Yes                 | 174.94.30.143/32     |
| Web-1     | No                  | 10.0.0.4             |
| Web-2     | No                  | 10.0.0.4             |
| ElkVM     | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for a quick removal and relaunching of the server if it is compromised. 

The playbook implements the following tasks:
- Increases the available use of virtual memory necesssary for collecting logs
- Downloads and launches a docker elk container with available ports (5601:5601, 9200:9200, 5044:5044)
- Installs Python so that the container can run
- Forces docker to boot whenever the server is restarted

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Diagrams/Elk Container Deployment.JPG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed Filebeat on both of these machines. This Beat allow us to collect system logs, which can be used to track logon events among other system processes.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to the /etc/ansible/ directory in the ansible container on the Jump Box.
- Update the hosts file to include the IPs of the targeted machines (IPs for Filebeat are listed under "webservers" while the IP for the Elk server is listed under "elk")
- Run the playbook, and navigate to http://104.40.12.162:5601/app/kibana to check that the installation worked as expected.
