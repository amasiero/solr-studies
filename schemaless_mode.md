# create and copy configsets
```
cd $solr_home

cd server/solr/configsets
mkdir search_twitter
cp -r _default/. search_twitter
```

# create a solr core with default configs
```
curl -X GET 'http://localhost:8983/solr/admin/cores?action=CREATE&name=search_twitter&instanceDir=configsets/search_twitter'
```
# get current schema fields
```
curl -X GET "http://localhost:8983/solr/search_twitter/schema/fields"
```
# add document to solr
```
curl -X POST -H 'Content-Type: application/json' 'http://localhost:8983/solr/search_twitter/update' --data-binary '
{
  "add": {
    "doc": {
        "content":"Late night with Solr 8.5",
        "likes":10
	}
  }
}'
```
# get current schema fields
```
curl -X GET "http://localhost:8983/solr/search_twitter/schema/fields"
```
# delete a collection
```
curl -X GET 'http://localhost:8983/solr/admin/cores?action=UNLOAD&core=search_twitter&deleteInstanceDir=true&deleteDataDir=true'
```
