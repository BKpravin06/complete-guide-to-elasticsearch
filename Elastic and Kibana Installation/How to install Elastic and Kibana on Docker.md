
**How How to install Elastic and Kibana on Docker**


1. docker network create elastic

2 **docker run -d --name elasticsearch \
  --net elastic \
  -p 9200:9200 \
  -e "discovery.type=single-node" \
  docker.elastic.co/elasticsearch/elasticsearch:8.12.0**

# OR

**docker run -d --name elasticsearch \
  --net elastic \
  -p 9200:9200 \
  -e "discovery.type=single-node" \
  -e "xpack.security.enabled=true" \
  -e "ELASTIC_PASSWORD=changeme" \
  docker.elastic.co/elasticsearch/elasticsearch:8.12.0**

############################################################

3. **docker run -d --name kibana \
  --net elastic \
  -p 5601:5601 \
  -e "ELASTICSEARCH_HOSTS=http://elasticsearch:9200" \
  docker.elastic.co/kibana/kibana:8.12.0**

once it installed, check the below command

**docker ps -a** :- two container will be created one for Kibana and other one for Elasticsearch

start both of the container using below Command

**docker start conatiner-id**

once container up and running then goto the browser and hit the below url
**http://localhost:5601**

Once you hit the above URL it will ask you for the **token no.**, then go to the server and hit the below command and copy the token and paste it on the browser.

**docker exec -it elastic conatiner-id bin/elasticsearch-create-enrollment-token -s kibana**

After thet it will ask you for the **verification code** for that run the below command on your server and it will be show you the verification code on the screen
paste that code on the browser   

**docker exec -it kibana container-id bin/kibana-verification-code**

It will ask you for the User Name and Passowrd, for that please run the below command for creating auto password

**docker exec -it elasticsearch bin/elasticsearch-setup-passwords auto**

User Name :- elastic

