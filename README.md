## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


  - [Cloud Network Diagram](https://github.com/hart2533/ELK-Stack-Project/blob/main/Diagrams/Final-Cloud-Diagram.png)

  - [Cloud Diagram with ELK](https://github.com/hart2533/ELK-Stack-Project/blob/main/Diagrams/Final-ELK-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Beat file may be used to install only certain pieces of it, such as Filebeat.

  - [Filebeat Playbook](https://github.com/hart2533/ELK-Stack-Project/blob/main/Ansible/Filebeat/filebeat-playbook.yml)


**This document contains the following details:**
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable, in addition to restricting traffic to the network.

- Load balancers can defend an orgainization against denial-of-service (DDos) attacks by shifting from a private server to a public cloud provider. The main advantage of using a jump-box are the hardened security it provides, and the ability to manage other virtual machines within a network or security zone. 



Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat monitors locations and log files, collects log event data, and sends that data to Elasticsearch.


- Metricbeat documents the statistics and metrics that it collects, and sends them to an output. (For example, Elasticsearch)


The configuration details of each machine may be found below.

| Name     |  Function  | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.4   | Linux            |
| Web-1    |Webserver 1 | 10.0.0.5   | Linux            |
| Web-2    |Webserver 2 | 10.0.0.6   | Linux            |
| Web-3    |Webserver 3 | 10.0.0.7   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump-box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- 52.188.14.223

Machines within the network can only be accessed by jump-box VM.

- Web-1 VM is the only VM able to access the ELK VM.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 52.188.14.223        |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| Web-3    | No                  | 10.0.0.4             |
| Web-ELK  | No                  | 10.0.0.7             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- using Ansible to automate routine or daily tasks allows the administrator to spend more time on important tasks. 

The playbook implements the following tasks:
- Install Docker
- Install python3.pip
- Install Docker python module
- Increase memory
- Download and launch a docker elk container. 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

  - [ps Output](https://github.com/hart2533/ELK-Stack-Project/blob/main/Ansible/Images/Output-ps.png)



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 (Web-1)
- 10.0.0.6 (Web-2)
- 10.0.0.7 (Web-3)

We have installed the following Beats on these machines:


- [Filebeat-Playbook](https://github.com/hart2533/ELK-Stack-Project/blob/main/Ansible/Filebeat/filebeat-playbook.yml)
  - [Filebeat-Configuration](https://github.com/hart2533/ELK-Stack-Project/blob/main/Linux/Filebeat/filebeat-configuration.yml)
- [Metricbeat-Playbook](https://github.com/hart2533/ELK-Stack-Project/blob/main/Ansible/Metricbeat/metricbeat-playbook.yml)
  - [Metricbeat-Configuration](https://github.com/hart2533/ELK-Stack-Project/blob/main/Linux/Metricbeat/metricbeat-configuration.yml)


These Beats allow us to collect the following information from each machine:
- These beats allow us to monitor the logs and locations specified by the user in order to keep track of changes made to a log file. They also allow us to keep record of stats and metrics from the services running on the server; also, those recorded from the operating system. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible.cfg file to /etc/ansible.
- Update the ansible.cfg file to include the IP addresses to be addes as hosts. 
-   For example, "<IP_Address> ansible_python_interpreter=/usr/bin/python3"


- Run the playbook, and navigate to http://52.173.16.222:5601/app/kibana to check that the installation worked as expected.

- The Filebeat Playbook is saved /etc/ansible/filebeat-playbook.yml, and it is also copied to /etc/filebeat/filebeat.yml
- Update the /etc/ansible/filebeat-playbook file to make Ansible run a playbook on a specific machine by adding that machine name and private IP Address to the hosts in the playbooks config file. 

- Nativate to http://52.173.16.222:5601/app/kibana

### Updating /etc/ansible/hosts
- Navigate to the [webservers] paragraph. On the next line directly under webservers add the following:
  - 10.0.0.4 ansible_python_interpreter=/usr/bin/python3
  - 10.0.0.5 ansible_python_interpreter=/usr/bin/python3
  - 10.0.0.6 ansible_python_interpreter=/usr/bin/python3
- Next, create a new section for [elk] hosts. On the next line directly below, the following server will be added:
  - 10.1.0.5 ansible_python_interpreter=/usr/bin/python3


### Using Kibana
- Kibana is an interface is used to research evens that have happened on a network. Any attack leaves a trace that can be followed and investigated using logs. 
- Using Kibana, you can categorize the data by using timestamps, geographic location, or even more specific fields suchs as response code to see if any user had an error and which error was presented. 
  - Overview of data panes:
    - **Unique Visitors:** Unique visitors to the website for the time frame specified.
    - **Source Country:** Web traffic by country.
    - **Visitors by OS:** The kind of OS visitors are using.
    - **Response Codes Over Time:** HTTP response codes 200, 404 and 503.
    - **Unique Visitors vs. Average Bytes:** The number of visitors and the amount of data they use.
    - **File Type Scatter Plot:** A graph showing the types of files that were accessed.
    - **Host, Visits and Bytes Table:** A table showing the kinds of files that were accessed.
    - **Heatmap:** Hours of the day that are most active by country.
    - **Source and Destination Sankey Chart:** Connections that have been made by country. The thicker the line, the more data was transferred between machines.
    - **Unique Visitors by Country:** Countries the traffic is originating from.


## Commands to Use the Playbook
- cd /etc/ansible
  - Move into the correct location.
- nano ansible.cfg
  - add host username to the correct location.
  - Ctrl + x to exit the file.
- nano hosts
  - add the machine, ip address and the ansible_python-interpreter=/usr/bin/python3 to the hosts.
  - Ctrl + x to exit the file.
- nano install_elk.yml 
  - Add your machine name to the correct location.
  - Ctrl + x to exit the file.
- To run the playbook use the following command: 
  - ansible-playbook install-elk  (ansible-playbook <yml filename>)
  
