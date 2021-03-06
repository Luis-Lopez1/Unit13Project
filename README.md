## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Filepath to diagram](Diagrams/Cloud_Security_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  - ![Filebeat-playbook file](Ansible/Filebeat/filebeat-playbook.yml)

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
- _Load balancing distributes network traffic, prevenenting failure(s) caused by overloading a particular resource (for example a dos attack). A jumpbox allows for managing access and security._

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- _Filebeat monitors the log files, log events, or locations that you specify._
- _Metricbeat collects metrics from the system and services running on the server._

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System     |
|----------|----------|------------|----------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux (ubuntu 18.04) |
| Web-1    | VM       | 10.0.0.5   | Linux (ubuntu 18.04) |
| Web-2    | VM       | 10.0.0.6   | Linux (ubuntu 18.04) |
| ELKvm    | VM       | 10.1.0.4   | Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _My public ip: 68.228.89.25_

Machines within the network can only be accessed by ssh.
- _We allowed the machine JumpBoxProvisioner to access our ELK VM. It's IP address is 10.0.0.4_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 68.228.89.25         |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| ELKvm    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _If we were to add new virtual machines, we can apply for same ruleset for each of them; automation of code._

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- 1. Install Docker
- 2. Install python3-pip
- 3. Increase Virtual Memory (sysctl -w vm.max_map_count=262144)
- 4. Install elk container
- 5. Enable docker to start on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Filepath to docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _Web-1 (10.0.0.5) and Web-2 (10.0.0.6)_

We have installed the following Beats on these machines:
- _Filebeat and Metricbeat_

These Beats allow us to collect the following information from each machine:
- _Filebeat collects audit logs, deprecation logs, gc logs, server logs, and slow logs._
- _Metricbeat collects metrics and statistics from the system and services running on the server._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the /etc/ansible/files/filebeat-config.yml file to /etc/filebeat/filebeat.yml.
- Update the config file to include elkserver ip for output.elasticsearch and setup.kibana.
- Run the playbook, and navigate to Kibana (http://[ELKvmPublicIP]:5601/app/kibana#) to check that the installation worked as expected.
