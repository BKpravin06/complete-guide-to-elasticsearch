**To view CPU and memory data of another Linux system in your Kibana**

1. Please check elastic is already running or not in your New system, If not then please Install first

systemctl status metricbeat.service

**Install Metricbeat on the Remote Linux System**

On the target Linux machine (whose CPU/memory you want to monitor)

wget https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-8.12.0-x86_64.rpm

rpm -vi metricbeat-8.12.0-x86_64.rpm

2. Configure Metricbeat

**Edit the config file**

vi /etc/metricbeat/metricbeat.yml

Set Elasticsearch Output (your main server IP)

output.elasticsearch:

  hosts: ["http://<ELASTIC_IP>:9200"]

  username: "elastic"
  
  password: "your_elastic passowrd"
  
  ssl.verification_mode: none   **if you are not using any cert.**

  3. Enable System Module (CPU & Memory)

   metricbeat modules enable system
  
  **Edit module config**

  vi /etc/metricbeat/modules.d/system.yml

 **Ensure this is enabled:**

- module: system
  period: 10s
  metricsets:
    - cpu
    - memory
    - network
    - process
  
  4. Setup Kibana Dashboards (One-time)

  metricbeat setup
  
This loads dashboards into Kibana automatically.

If you are getting any error after hit **metricbeat setup** command, then try to fix this first.

**Error**:- Exiting: couldn't connect to any of the configured Elasticsearch hosts. Errors: [error connecting to Elasticsearch at

5. Open Firewall

sudo firewall-cmd --list-ports

sudo firewall-cmd --add-port=5601/tcp --permanent   **Check which port are using 9200 or 6501**

sudo firewall-cmd --reload

 once done try to ping the elastic IP and Telnet as well

6. Check If Elasticsearch Uses HTTPS (VERY COMMON

curl -k https://192.168.168.128:9200 or curl -k http://192.168.168.128:9200

if anoything is work then make a changes accrodingly on the file **refer the point no. 2(Configure Metricbeat)**

**I have made a changes in my metricbeat file accordingly**

<img width="893" height="998" alt="image" src="https://github.com/user-attachments/assets/9dbb6160-c4a5-467e-a405-f43e23114395" />


7. Check Elasticsearch Binding (IMPORTANT)

**On Elasticsearch server:**

vi /etc/elasticsearch/elasticsearch.yml  or  docker exec -it <container_name_or_id> bash/usr/share/elasticsearch/config/elasticsearch.yml

Make sure:

network.host: 0.0.0.0

8. Check Docker Port Mapping on your main server

docker ps

**Look for Kibana container:**

0.0.0.0:5601->5601/tcp

If using docker run

docker run -d \
  --name kibana \
  -p 5601:5601 \
  docker.elastic.co/kibana/kibana:8.12.0

  **test again from your Machine**

  curl http://IP of server:5601  or curl http://IP of server:9200

  and Update the your metricbeat file accordingly with above IP and port no.

  metricbeat setup to check if it ok or not

  Mostly this issue will help to fix your issue

  
<img width="303" height="146" alt="image" src="https://github.com/user-attachments/assets/dbf834a9-4730-490a-be3a-c564724c5e7c" />

<img width="1229" height="222" alt="image" src="https://github.com/user-attachments/assets/7e00adad-9271-44c5-b9ab-7d80fb5736e2" />

<img width="1511" height="866" alt="image" src="https://github.com/user-attachments/assets/2e0fe295-2ffa-49a5-8096-6199c7b89e43" />






  

  

  
