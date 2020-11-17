# Brian-Williams-Elk-Server-Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Image of elk network](https://github.com/bwilliams4428/My-Elk-Server-Project/blob/main/Diagrams/Elk-server-project-topology.png)
![Image of elk network](https://github.com/bwilliams4428/My-Elk-Server-Project/blob/main/Diagrams/azuretopology.PNG)
![Image of elk network](https://github.com/bwilliams4428/My-Elk-Server-Project/blob/main/Diagrams/azuretopology2.PNG)
![Image of elk network](https://github.com/bwilliams4428/My-Elk-Server-Project/blob/main/Diagrams/azuretopology3.PNG)
![Image of elk network](https://github.com/bwilliams4428/My-Elk-Server-Project/blob/main/Diagrams/azuretopology4.2.PNG)
![Image of elk network](https://github.com/bwilliams4428/My-Elk-Server-Project/blob/main/Diagrams/azuretopology5.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML playbook file may be used to install only certain pieces of it, such as Filebeat.

The playbook files to install Elk, Filebeat and Metricbeat are accessible below:
  * [install-elk.yml](https://github.com/bwilliams4428/My-Elk-Server-Project/blob/main/Ansible/install-elk-.yml)
  * [filebeat-playbook.yml](https://github.com/bwilliams4428/My-Elk-Server-Project/blob/main/Ansible/filebeat-playbook.yml)
  * [metricbeat-playbook.yml](https://github.com/bwilliams4428/My-Elk-Server-Project/blob/main/Ansible/metricbeat-playbook.yml)
  
### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive and available, in addition to restricting access to the network.

  What aspect of security do load balancers protect? 
    
    A load balancer can provide a web application firewall to protect the application from malicious actors, detect and block DDoS attacks and authenticate  
    user access by requesting a username and password from the client device. With regard to the CIA triad, a load balancer ensures availablity.

  What is the advantage of a jump box?
    
    The jumpbox controls access to machines on the private network. It allows access from specific IPs that are granted access in the network's firewall rules.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system logs and system metric data.
   
   What does Filebeat watch for? 
   
    Filebeat watches for changes to system and application log files.
   
   What does Metricbeat record? 
   
    Metricbeats records system metric data from the operating system installed on the server and running services on the server. Examples of the data that     
    metricbeats records are CPU and RAM usage data, inbound and outbound network traffic and the number of processes running on the server. 
    
The configuration details of each machine may be found below.

| Name                | Function   | IP Address   | Operating System      |
|---                  |---         |---           |---                    |
| TheeRedJumpbox      | Gateway    | 10.1.0.4     | Linux (ubuntu 18.04)  |
| Thee-Red-Team-Web1  | DVWA       | 10.1.0.5     | Linux (ubuntu 18.04)  |
| Thee-Red-Team-Web2  | DVWA       | 10.1.0.6     | Linux (ubuntu 18.04)  |
| Thee-Red-Team-Web3  | DVWA       | 10.1.0.7     | Linux (ubuntu 18.04)  |
| ELK-Web             | ELK        | 10.0.0.5     | Linux (ubuntu 18.04)  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the TheeRedJumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
   My resedential IP address

Machines within the network can only be accessed by SSH through the Ansible container.
   Which machine did you allow to access your ELK VM? 
      TheeRedJumpbox is allowed to access my ELK-Web VM
   
   What was its IP address?
       10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Address   |
|---                  |---                  |---                   |
| TheeRedJumpbox      | Yes/No              | My residential IP    |
| Thee-Red-Team-Web1  | No                  | 10.1.0.4             |
| Thee-Red-Team-Web2  | No                  | 10.1.0.4             |
| Thee-Red-Team-Web3  | No                  | 10.1.0.4             |
| ELK-Web             | Yes/No              | My residential IP and 10.1.0.4   |    

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
    
   What is the main advantage of automating configuration with Ansible?
       The main advantage of automating configuration with Ansible is that it is easy to use. YAML, the language that used by Ansible playbooks, is an easily  
       readable language that can be comprehended by non-techically inclined individuals. Ansiblee can configure and deploy services on multiple servers and 
       systems in far less time than manual deployment and configuration. 

The playbook implements the following tasks:

In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.
    
 * Create a Virtual Machine that will host the ELK server. The VM should have a public IP to access Kibana from our personal IP
 * Add the ELK server's private IP to  Ansible's hosts file under a category to identify the private IP with the ELK server (Ex. [elkservers])
 * Create an Ansible playbook file (.yml) that will install docker, python, download and launch ELK container on the ELK VM. 
 * You can create additioanal playbooks files to install Filebeat and Metricbeat
 * Access the ELK server from the VM's public IP on port 5601

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Image of elk container running](https://github.com/bwilliams4428/Brian-Williams-Elk-Server-Project/blob/main/Diagrams/docker_ps_output.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 
List the IP addresses of the machines you are monitoring

	* 10.1.0.5
	* 10.1.0.6
	* 10.1.0.7
	
We have installed the following Beats on these machines:

Specify which Beats you successfully installed

	* Filebeat
    * Metricbeat
	
These Beats allow us to collect the following information from each machine:

In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

	Filebeat monitors system log files and locations specified by the system admin, documents the log events and sends them to the ELK server for indexing. Filebeat logs SSH logins from servers
	systems or virtual machines that it was setup to monitor.
	
	![Image of elk container running](https://github.com/bwilliams4428/Brian-Williams-Elk-Server-Project/blob/main/Diagrams/docker_ps_output.PNG)
	
	Metricbeats records system metric data from the operating system installed on the server and running services on the server. Examples of the data that     
    metricbeats records are CPU and RAM usage data, inbound and outbound network traffic and the number of processes running on the server.

	![Image of elk container running](https://github.com/bwilliams4428/Brian-Williams-Elk-Server-Project/blob/main/Diagrams/docker_ps_output.PNG)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the config files for Filebeat and Metricbeat after downloading them using the curl command to /etc/ansible/roles.
		* [filebeat-config.yml](https://github.com/bwilliams4428/Brian-Williams-Elk-Server-Project/blob/main/Ansible/install-elk-.yml)
        * [metricbeat.yml](https://github.com/bwilliams4428/Brian-Williams-Elk-Server-Project/blob/main/Ansible/filebeat-playbook.yml)

- Update the output.elasticsearch and setup.kibana parameters in both config files to use the private IP for the ELK server virtual machine.

- Run the playbook, and SSH to the ELK VM. Run sudo docker ps to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_

Which file is the playbook? 
  
  * [filebeat-playbook.yml](https://github.com/bwilliams4428/Brian-Williams-Elk-Server-Project/blob/main/Ansible/filebeat-playbook.yml)
  * [metricbeat-playbook.yml](https://github.com/bwilliams4428/Brian-Williams-Elk-Server-Project/blob/main/Ansible/metricbeat-playbook.yml)


Where do you copy it?_
   
   /etc/ansible/
   
Which file do you update to make Ansible run the playbook on a specific machine? 
   
   * [filebeat-config.yml](https://github.com/bwilliams4428/Brian-Williams-Elk-Server-Project/blob/main/Ansible/install-elk-.yml)
   * [metricbeat.yml](https://github.com/bwilliams4428/Brian-Williams-Elk-Server-Project/blob/main/Ansible/filebeat-playbook.yml)
    
    Change the output.elasticsearch and setup.kibana parameters in both config files to use the private IP for the specific machine.     
	

How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

	Inside the /etc/ansible directory is a file named hosts.cfg. That file has parameters for webservers, elkservers and other server types. In the install-elk playbook file, 
	set the hosts parameter to elkservers so that the playbook knows to install the elk server container on the server that uses the elkservers parameter.

Which URL do you navigate to in order to check that the ELK server is running?

	http://168.61.186.22:5601/

**Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
  
	* ssh username@publicJumpBoxIP
	* sudo docker container ls -a
	* sudo docker start (container ID number or name)
	* sudo docker attach (container ID number or name)
	* cd /etc/ansible
	* open the hosts.cfg file in a text editor and input the private IP for the ELK server under the elkservers parameter 
	* download the Filebeat and/or Metricbeat config file using curl and store it locally (Ex. curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml) 
	* change the output.elasticsearch and setup.kibana parameters to use the private IP for your ELK VM
	* create a playbook file (filebeat-playbook.yml) and specify the server type that the container will install on in the hosts paramter of the playbook file
	* run ansible-playbook filebeat-playbook.yml 
	* access http://publicIPforELKVM:5601 from a web browser, click on 'Logs' from the Kibana menu to see Filebeat in action
	
	The same process applies to Metricbeat. You will need to change file names to use Metricbeat, the URL to download the config file and click on 'Metrics' from the Kibana menu to see that beat in action.
