**After Import data from Github and everything looks normal then use below command to check the data**

1. **User the below command to check your data**
   
GET /indexname/_search
{
  "query": {
    "match_all": {}
  }
}

3. **check the status of the docke-cluster status**
   
GET /_cluster/health

If status showing in **Yellow** then please run the below command to make it **Green**


PUT _all/_settings
{
  "number_of_replicas": 0
}
