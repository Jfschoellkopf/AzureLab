# AzureLab
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Red_Team_resource_Diagram](https://user-images.githubusercontent.com/83138086/134306154-aebfa6bd-3b78-42b6-ae7c-b41c85ee7157.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YALM files may be used to install only certain pieces of it, such as Filebeat.

  - /etc/ansible/elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting access to the network.

What aspect of security do load balancers protect?
        Load balancers evenly distribute HTTP traffic to the servers, preventing server attacks such as DDoS attacks.
What is the advantage of a jump box?
        Jump boxes provide secure connection to the server

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
        What does Filebeat watch for?
        Filebeat watches for changes by collecting and logging files and events; forwarding them to Kibana for analysis.
        What does Metricbeat record?
        Metricbeat is installed on a host to monitor and record performance metrics.
The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name          | Function    | IP Address  | Operating System |
|---------------|-------------|-------------|------------------|
| Jump Box      | Gateway     | 10.0.0.1    | Linux            |
| Web1-DVWA     | Webserver   | 10.0.0.5    | Linux            |
| Web2-DVWA     | Webserver   | 10.0.0.6    | Linux            |
| ELK-Server    |ELK Server   | 10.1.0.4    | Linux            |
| Load Balancer |Load Balancer| 52.150.8.188| Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the ELK Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Workstation 13.89.51.194 through TCP on port 5601.

Machines within the network can only be accessed by workstation and the jumpbox.
- Which machine did you allow to access your ELK VM? What was its IP address?
  I used Jump-Box-Provisioner IP 20.102.84.195 SSH port 22 to access my ELK VM and its IP address is 13.89.51.194

A summary of the access policies in place can be found in the table below.

| Name         | Publicly Accessible | Allowed IP Addresses |
|--------------|---------------------|----------------------|
| Jump Box     | Yes                 | 20.102.84.195        |
| Web1-DVWA    | No                  | 10.0.0.5             |
| Web2-DVWA    | No                  | 10.0.0.6             |
| ELK Server   | Yes                 | 13.89.51.194         |
| Load Balancer| Yes                 | 52.150.8.188         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
  Ansible will quickly make changes to the system, rather than doing each one manually.

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.
... Install docker.io
... Install pip3
... Install Docker python module
... Increase virtual memory
... Download and Launch Docker


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

        /c/Users/17163/Downloads/Docker.ps_command.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines the Elk_Server is configured to monitor:
        Web1-DVWA: 10.0.0.5
        Web2-DVWA: 10.0.0.6
We have installed the following Beats on these machines:
        FileBeats
        MetricBeats

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.

        FileBeats are used as a lightweight shipper for forwarding and centralizing log data. The data FileBeat collects is about changes in the filesystem. An example of a FileBeat are Apache Access Logs that can be used for monitoring traffic to your service.
        MetricBeats collect machine metrics, such as uptime. They are installed on different servers in my environment and are used for monitoring performance.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and filebeat-playbook.yml file to the /etc/Ansible/ directory.
- Update the hosts file to include the host IP address in filebeat-config.yml file.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?
        elk.yml and it is located inside /etc/ansible/elk.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
        I would update my hosts file in /etc/ansible/hosts  and I would be able to specify which machine to install the ELK server and Filebeat on by running nano hosts, and adding the installer-python or filebeat under [webervers] or [elk].
- _Which URL do you navigate to in order to check that the ELK server is running?
        I would navigate to my Kibana URL: http://13.89.51.194:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
cd /etc/ansible curl -i href="https://github.com/Jfschoellkopf/AzureLab.git" ansible-playbook /etc/ansible/elk.yml
