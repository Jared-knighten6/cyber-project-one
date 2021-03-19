## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/Jared-knighten6/cyber-project-one/tree/main/Ansible/PlayBook

This document contains the following details:
- Description of the Topology

- Access Policies

- ELK Configuration
  - Beats in Use
  - Machines Being Monitored

- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to filtering access to the network.

- Load balancing ensures that the application will be highly available and adds resiliency by
  distributing live traffic evenly across multiple servers, effectively eliminating single points
  of failure from attacks such as DDoS attacks.

-  The advantage of the Jump Box is that it provides a gateway router to the private network,
  ensuring that all other machines in the network do not directly face the internet, providing
  a more secure network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them
  either to Elasticsearch or Logstash for indexing. The data can be viewed and analyzed with Kibana.
  
- Metricbeat collects metrics from the operating system and from services running on the server.
  Metricbeat then takes the metrics and statistics that it collects and ships them to Elasticsearch to be
  processed by Logstash, and can be viewed and analyzed with Kibana.

The configuration details of each machine may be found below.

| Name   | Function  | IP Address   | OS  |   |
|---|---|---|---|---|
| Jump Box   | Gateway  | 10.0.0.4  | Linux   |   |
| Web 1 DVWA   | Server   | 10.0.0.7   | Linux   |   |
| Web 2 DVWA  | Server   | 10.0.0.8   | Linux   |   |
| Web 3 DVWA   | Server   | 10.0.0.9  | Linux   |   |
| ELK-SERVER   | Monitoring The Servers  |  10.1.0.4  | Linux   |   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- The Jump Box Machine may be accessed from IP address 40.76.36.106

Machines within the network can only be accessed by the jump box.
- The ELK server may be accessed from the Jump Box Machine // 10.0.0.4

A summary of the access policies in place can be found in the table below.

|  Name  | Publicly Accessible  | Allowed IP Addresses  |
|---|---|---|
| Jump Box  | Yes  | 40.76.36.106  |
| Web 1 DVWA   | No  | 10.0.0.4  |
|  Web 2 DVWA | No  | 10.0.0.4  |
| Web 3 DVWA   | No  | 10.0.0.4  |
| ELK-SERVER   | No  | 10.0.0.4  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

-  Automating configuration with ansible ensures provisioning scripts run identically everywhere,
  every time they run. This eliminates as much variability between configurations as possible,
  and allows for easy installation of multiple versions of a tool(s) to be used at the same time
  accross different projects.

The playbook implements the following tasks:
- Configure Elk VM with Docker
- Install pip3
- Install Docker python module
- Install docker.io
- Download and launch a Docker elk container sebp/elk:761

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| Name  | IP Address  |
|---|---|
| Web 1 DVWA   | 10.0.0.7  |
| Web 2 DVWA   | 10.0.0.8  |
| Web 3 DVWA   | 10.0.0.8  |

We have installed the following Beats on these machines:
- Filebeat 
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat plays the role of the logging agent; installed on the machine generating the log files,
  tailing them, and forwarding the data to either Logstash for more advanced processing or directly
  into Elasticsearch for indexing.
  
  - Metricbeat is used for monitoring server performance within an environment, as well as
  different external services running on them. Like, Metricbeat can be used to monitor and
  analyze system CPU, memory and load.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Filebeat and Metricbeat configuration files to '/etc/ansible/'
- Update the configuration files to include your ELK-SERVER's private IP address: 
  
   - nano filebeat-config.yml
   - go to line 1106 & 1806
   - Update these lines with the ELk-SERVERS IP
              
        --------Next-------
              
    - nano metricbeat-config.yml
    - go to line 62 & 96
    - Update these lines with the ELk-SERVERS IP
    

- Copy Filebeat-playbook.yml to "/etc/ansible"

- Copy Metricbeat-playbook.yml to "/etc/ansible"

- To make Ansible run the playbook on a certain machine, you'll need to update the the "/etc/ansible/hosts" file to include: 

- Group Name -- [webservers] // [elk]

- Private IP addresses of the disired webservers & Location of Python 3 Interpreter -- "YourWebseversIP(x.x.x.x) ansible_python 3 interpreter"

- To run playbooks "ansible-playbook [Name_of_playbook.yml"

- After running each playbook you now can go to your ELK-SERVER

- Address of ELK-SERVER - http://[your.ELK-VM.External.IP]:5601/app/kibana
