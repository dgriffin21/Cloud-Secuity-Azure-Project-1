## Automated ELK Stack Deployment
 
The files in this repository were used to configure the network depicted below.
 
![Network Diagram](https://user-images.githubusercontent.com/81546221/134252735-f87d4fe8-2239-4974-acb5-cec1795d2aec.JPG)
 
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook files may be used to install only certain pieces of it, such as Filebeat, Metricbeat or ELK.
 
  - [Install Flebeat-Playbook.yml](https://github.com/dgriffin21/Cloud-Secuity-Azure-Project-1/blob/main/Ansible/Filebeat-Playbook)
  - [Install Metricbeat-Playbook.yml](https://github.com/dgriffin21/Cloud-Secuity-Azure-Project-1/blob/main/Ansible/Metricbeat-Playbook.yml)
  - [Install ELK-Playbook.yml](https://github.com/dgriffin21/Cloud-Secuity-Azure-Project-1/blob/main/Ansible/ELK-Playbook.yml) 
  
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build
 
 
### Description of the Topology
 
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
 
Load balancing ensures that the application will be highly effective and reliable, in addition to restricting access to the network. Load balancers provide additional layers of security the system, by balancing the incoming traffic to prevent DDOS attacks, thereby 
providing a more efficient application. While a Jump box is a gateway that filters out undesired traffic and allows access to IP addresses that have been whitelisted.
 
 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metrics and system logs.
- _Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing._
- _Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash._
 
The configuration details of each machine may be found below.

| Name     | Function      | IP Address   | Operating System |
|----------|---------------|--------------|------------------|
| Jump Box | Gateway       | 10.0.0.4     | Linux            |
| Web-1    | Web Server    | 10.0.0.5     | Linux            |
| Web-3    | Web Server    | 10.0.0.6     | Linux            |
| ELK      | ELK Container | 10.1.0.4     | Linux            |
| Load Bal |Balance traffic| 104.42.97.205| Linux            |
 
### Access Policies
 
The machines on the internal network are not exposed to the public Internet.
 
Only the JumpBoxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Public IP: Personal PC Public IP or Client IP
 
Machines within the network can only be accessed by JumpBoxProvisioner, IP 10.0.0.4, 104.42.34.69.

 
A summary of the access policies in place can be found in the table below.
 
| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | Public IP/Client     |
| Web-1    | No                  | 10.0.0.4             |
| Web-3    | No                  | 10.0.0.4             |
| ELKSErver| No                  | 10.0.0.4             |

### Elk Configuration
 
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because of the simple syntax used in creating the playbooks in YAML. The playbook implements the 
following tasks: 

- Install Docker.io
- Install Python3-pip 
- Use pip module to install docker module
- Increase virtual memory and memory usage
- Download and launch docker web container

 The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
 
![ELK Container Sucess](https://github.com/dgriffin21/Cloud-Secuity-Azure-Project-1/blob/main/Images/Docker_ELK_Container.JPG)
 
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 (Web-1)
- 10.0.0.6 (Web-3) 
 
We have installed the following Beats on these machines:
- Filebeat
- Metricbeat
 
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
 
SSH into the control node and follow the steps below:
- Copy the [Install ELK-Playbook.yml](https://github.com/dgriffin21/Cloud-Secuity-Azure-Project-1/blob/main/Ansible/ELK-Playbook.yml) file to /etc/ansible/ directory.
- Update the /etc/ansible/host file to include the private IP addresses of the machines you want ansible to run the playbook on.
- Run the playbook, and navigate to (40.114.27.46:5601) or (your-ELKServer-IP:5601) to check that the installation worked as expected.

![ELK Dashboard](https://github.com/dgriffin21/Cloud-Secuity-Azure-Project-1/blob/main/Images/ELK-Dashboard.JPG)
 
SSH into JumpBoxProvisioner from Local Desktop: 

- ssh azadmin@104.42.34.69
    
View list of docker containers: 
- sudo docker container list -a
    
  
Start docker: 
- sudo docker start happy_shamir
    
  
Attach to docker: 
- sudo docker attach happy_shamir
    
  
Add Webservers to hosts file: 
- nano /etc/ansible/hosts
- add additional private IPs under [webservers]
    
  
Run playbook to update elk: 
- ansible-playbook /etc/ansible/install-elk.yml
    
  
Copy filebeat configuration file: 
- copy filebeat-config.yml file to /etc/ansible/files/
    
Run playbook for filebeat: 
- ansible-playbook /etc/ansible/filebeat-playbook.yml
