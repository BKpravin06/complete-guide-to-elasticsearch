**Install and Configure Heartbeat agent on the server**

1. Install Heartbeat agent on the server

For CentOD - sudo rpm -vi https://artifacts.elastic.co/downloads/beats/heartbeat/heartbeat-8.12.0-x86_64.rpm

2. Configure heartbeat.yml file

   /etc/heartbeat/heartbeat.yml

output.elasticsearch:

  hosts: ["https://localhost:9200"]    #Kibana server IP
  
  username: "elastic"
  
  password: "YOUR_PASSWORD"
  
  ssl.verification_mode: none

3. Setup Heartbeat using below Command

   heartbeat setup

4. Once All done then goto Kibana :- Stack Management :- Data View :- Create Data view and Heartbeat will be showing there enter the name and select that one
5. Now Goto Discover and select Heartbeat Data will be visible on the Dashboard

  
   
