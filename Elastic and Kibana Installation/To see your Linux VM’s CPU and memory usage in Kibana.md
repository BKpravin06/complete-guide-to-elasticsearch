**To see your Linux VM’s CPU and memory usage in Kibana, you need to make sure Metricbeat is properly collecting and sending system metrics to Elasticsearch. Then you can visualize them in Kibana.**

1. Make sure Metricbeat is running

sudo systemctl start metricbeat
sudo systemctl enable metricbeat

Check:

systemctl status metricbeat

2. Enable system metrics module

Metricbeat collects CPU & memory via the system module.

sudo metricbeat modules enable system

Edit config:

sudo vi /etc/metricbeat/modules.d/system.yml

**Make sure it includes:**

- module: system
  period: 10s
  metricsets:
  
    - cpu
    - memory
    - network
    - process
      
3. Configure output to Elasticsearch

Open:

sudo vi /etc/metricbeat/metricbeat.yml

Set:

**User your elastic IP if Metricbeat agent installed on another system**

output.elasticsearch:

hosts: ["http://<ELASTIC_IP>:9200"]

4. Test and load dashboards
   
metricbeat test config
metricbeat test output

Then load dashboards:

metricbeat setup

Restart:

sudo systemctl restart metricbeat

5. View CPU & Memory in Kibana

Go to Kibana → Discover and see in dropdown Metricbeat* is visible or not.

If Metricbeat not visible then Goto same steps and clock on create a New view and select or give a name Metricbeat and save it.

Once all done data will be visible on Kibana
