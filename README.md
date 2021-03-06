## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/85502226/122276479-67f15a00-cf17-11eb-980a-3b2ce1769875.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of this file may be used to install only certain pieces of it, such as Filebeat.

![install-elk.yml](https://github.com/AdrianCeg/Project-13/blob/main/Ansible/install-elk.yml)

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
- Load balancing refers to the process of distributing a set of tasks over a set of resources (computing units), with the aim of making their overall processing more efficient. Load balancing can optimize the response time and avoid unevenly overloading some compute nodes while other compute nodes are left idle. Load balancers protects the system from DDoS attacks by shifting attack traffic. The advantage of a jump box is to give access to the user from a single node that can be secured and monitored.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system metrics.
- Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function  | IP Address | Operating System |
|----------|-----------|------------|------------------|
| Jump Box | Gateway   | 10.1.0.4   | Linux            |
| Web-1    | Server    | 10.1.0.5   | Linux            |
| Web-2    | Server    | 10.1.0.5   | Linux            |
|Project-VM| Monitoring| 10.0.0.4   | Linux                 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 175.38.244.139

Machines within the network can only be accessed by Jump-Box-Provisioner.
- Only Jump-Box-Provinsioner and IP address is: 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible   | Allowed IP Addresses |
|------------|-----------------------|----------------------|
| Jump Box   | Yes                   | 175.38.244.139/32    |
| Web-1      | No, only via Jump Box | 10.1.0.4/32          |
| Web-2      | No, only via Jump Box | 10.1.0.4/32          |
| Project-VM | No, only via Jump Box | 10.1.0.4/32          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The primary benefit of Ansible is it allows IT administrators to automate away the drudgery from their daily tasks. That frees them to focus on efforts that help deliver more value to the business by spending time on more important tasks.

The playbook implements the following tasks:
- Install Docker.io
- Install pip3
- Install Docker python module
- Increase memory
- Download and launch a docker elk container thru ports: 5401; 9200; 5044.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/85502226/122276680-9e2ed980-cf17-11eb-94eb-c3196368275c.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.1.0.5
- Web-2 10.1.0.6

We have installed the following Beats on these machines:
- filebeat
- metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat periodically collect metrics from the operating system and from services running on the server, and as well takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to Ansible container folder /etc/ansible/files/
- Update the host file /etc/ansible/hosts to include Project-VM IP address: 10.0.0.4
- Run the playbook, and navigate to /etc/ansible/http://<VM IP>/:5601 to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- The playbook file is install-elk.yml and is copied in /etc/ansible
- Updating the host file will make Ansible run the playbook on a specific machine
- By adding a private IP under servers you can specify which machine to install and the Project-VM server on vs filebeat
- http://[your.VM.IP]:5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
