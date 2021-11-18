# WK13-ELK-Project
This repository will include diagrams, Linux and Ansible scripts, descriptions of each process.

# Cloud Network
The majority of scripts used were to enable/configure different cloud servers with docker containers for the virtual machines being used.

I started with a setup of the my Azure portal which allowed me to create my network starting with the creation of my Resource Group then added four virtual machines, virtual networks, load balancers (front end and back end) and network security groups. For each virtual machine, vnet, load balancers and resource group a private and public address was assigned to each one accordingly. 

Using the BASH command line I used my docker container to access my virtual machines using specific commands that enabled me to use ansible and .yml scripts to install filebeat and metricbeat. Finally connecting my jumpbox to connect to my repository in GitHub. Docker is a container that assists you when you create, deploy and run apps.

In the final step of the process we needed to use four servers that were running vulnerable DVWA containers. Included with the DVWA's were a jump-box and an ELK stack container.

I created a diagram that shows how my cloud network uses the jump-box, virtual machines, load balancers, and docker containers that were created. 
(see diagrams folder in github repository)


#Azure Portal Setup
- Created my account in Azure.com
- Created my resource group (go to resource group in search bar) in this case I called it: batmansknight, created a user name: azureuser
- Created my Virtual Machines which includes: jumpboxprovisioner, web-1, web-2, web-3, ELK-SERVER
- Each VM will have inbound security rules specific to their networks (SSH, deny-all).
- After creating all VM's the network security groups will need to be set up, in this case mine is: jumpboxprovisioner-nsg
- I created a public key which will be used to connect my network to the jump-box (see below for public key)


- Using Bash and the ssh -i ~/azurekey azureuser@0.0.0.0 command I can now access my jump-box.
  
# Bash Command Line and Commands for Containers, .yml Configurations and Playbooks
- Once inside the jump-box I use sudo su command to access root user
- From here I can create another public key that will be used for my VM's

- Now that I am in my Ansible Container I can access my docker container: priceless_jemison
  - To access the docker container priceless_jemison I used commands: docker start preceless_jemison, docker attach priceless_jemison then you will be root user: root@d106743a847e:~#

# Next is setting up the ELK container using a script.
  - The elk_config.yml will be located here: root@d106743a847e:/etc/ansible/playbooks# ls
ansible_config.yml  apacheInstallUninstall.yml  elk_config.yml  filebeat-playbook.yml  metricbeat-playbook.yml
  - The script should look something like this:
  Last login: Tue Nov 16 23:27:03 2021 from 10.0.0.4

         
  # Now that filebeat has been installed you can now connect to Kibana.
    - After running the script and installing the filebeat-playbook.yml you will go to Kibana using your ELK-SERVER public ip, mine is 104.40.74.253
    - After connecting to Kibana and selecting system logs and running the script you should be able to Check Data for your Module Status.
    - After connecting the data you will have sys logs running and tracking your data.

 # Filebeat is now connected. The next step is to configure, install and run metricbeat.
   - command to access metricbeat-playbook.yml: root@d106743a847e:/etc/ansible/playbooks#nano metricbeat-playbook.yml
   - Like the filebeat-config.yml you will change the IP addresses and ports to be: 10.1.0.4:9200, 10.1.0.4:5601
   - Next is to run the metricbeat-playbook.yml script
         
    - Similar to filebeat you will go to Kibana and select docker and connect to the Module Status to check data and connections.
    - At this point the filebeat and metricbeat are connected to Kibana which will allow you to see the traffic through graphs that are selected in Kibana. (see repository for diagrams)

# Load Balancers
 - Now I can attach my web -1, web-2 and web-3 to my backend loadbalancer: Gotham-BE-LB
 - This will help distribute traffic evenly through my web 1,2,3

# Creating an account for GitHub and syncing to GitHub through my command line.
 - Create an account at github.com, create a repository and commit a README.md file with a short sentence. Click on the Clone or Download button.
 - Use command git clone https://github.com/joehmeyers/SCRIPTS.git
       - Create a username and password
 - Run command git add . to sync all items in specified directory.
 - Then run git commit -m "First Commit" to confirm items with a short sentence.
 - Lastly, run command git push to sync all the content specified.
 - Check your github repository to assure the files are acurate.

# At this point all configurations, playbooks, VM's, containers, downloads and installations should be completed and working accordingly.
  








