# ELKStackDeployment
# Automated ELK Stack Deployment
The files in the repository were used to configure and deploy a live ELK deployment on Microsoft Azure.

#insert

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Azure Cloud Environment file may be used to install only certain pieces of it, such as Filebeat.

#filebeat file

This document contains the following details:

•	Description of the Topology

•	Access Policies

•	ELK Configuration 

-Beats in use
	
-Machines Being Monitored

•	How to Use the Ansible Build

# Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unauthorized traffic to the network.

  Load balancers offer an effective and cost wise defense to DDoS attacks.  The advantage of a jump box is to give access to the end user from one specfic node that can be secured and monitored. 

  Filebeat helps generate and organize log files to send to Logstash and Elasticsearch. Specifically, it logs information about the file system, including which files have changed and when.

  Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

  The configuration details of each machine may be found below. 

  | Name                 | Function       | IP Address | Operating System |
|----------------------|----------------|------------|------------------|
| Jump-Box-Provisioner | Gateway        | 10.0.0.7   | Linux            |
| Web-1                | DVWA Container | 10.0.0.8   | Linux            |
| Web-2                | DVWA Container | 10.0.0.9   | Linux            |
| Web-3                | DVWA Container | 10.0.0.10  | Linux            |
| ELK                  | Configuration  | 10.1.0.4   | Linux            |

| Application  | Version                              |
|--------------|--------------------------------------|
| Docker       | version 19.03.6                      |
| filebeat     | version 7.4.0 (amd64), libbeat 7.4.0 |
| metricbeat   | version 7.4.0 (amd64), libbeat 7.4.0 |

# Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

•	108.69.213.253 – my home computer

Machines within the network can only be accessed by the DVWA container in the Jump-Box-Provisioner VM.

•	Through a peering connection my home computer (108.69.213.253) and the    Jump-Box VM (10.0.0.7) are allowed access the ELK Server 

A summary of the access policies in place can be found in the table below.

| Name                 | Publicity Accessible | Allowed IP Address       |
|----------------------|----------------------|--------------------------|
| Jump-Box-Provisioner | Allow                | 10.0.0.7, 108.69.213.253 |
| Web-1                | Deny                 | 10.0.0.7                 |
| Web-2                | Deny                 | 10.0.0.7                 |
| Web-3                | Deny                 | 10.0.0.7                 |
| ELK                  | Deny                 | 10.0.0.7, 108.69.213.253 |


# Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

•	Simply stated, it lends to the reduction of human error and the automation of mundane tasks and spend more time focused on other issues. 

The playbook implements the following tasks:

•	Install Docker

•	Download Image

•	Configure Container

•	Create playbbok.yml files 

•	Run playbooks

The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

#insert command

# Target Machines & Beats

This ELK server is configured to monitor the following machines:

•	10.0.0.8 -Web-1

•	10.0.0.9 -Web-2

•	10.0.010- Web-3

We have installed the following Beats on these machines:

•	Filebeat

•	Metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat: After you start Filebeat, open the Logs UI and watch your files being tailed right in Kibana. Use the search bar to filter by service, app, host, datacenter, or other criteria to track down curious behavior across your aggregated logs.

#insert graph

Metricbeat: Takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

#insert graph

# Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

Navigate to /etc/ansible/files and use the curl command to add the config file:

https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml

•	Copy the filebeat-playbook.yml file to /etc/ansible/roles.

•	Update the filebeat-config.yml file to include the ELK server private IP in lines 1106 and 1806.

•	Run the filebeat-playbook.yml playbook and navigate to the kibana page at [ELK public IP]/app/kibana to check that the installation worked as expected.







