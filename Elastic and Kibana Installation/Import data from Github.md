
# If you have a already json file in your github repo then use the below stpes 

**Open the putty and hit the below command to download the json file from your repo**

**curl -O https://github.com/BKpravin06/complete-guide-to-elasticsearch/blob/main/recipes-bulk.json**

Once download the file please cross verify in your system.

Now we need to move/copy that file into our elastic conatiner

**docker cp recipes-bulk.json elasticsearch-container-id:/usr/share/elasticsearch/**

Once successfully the copy, please goto your elastic conatiner and cross verify using below command

**docker exec -it elasticsearch-container-id bash**


