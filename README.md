# Search-Engine

# General set up
1. Run docker compose
```
docker compose up --build -d
```

# 1. Upload configuration to zookeeper
```
docker exec -it solr1 /opt/solr-8.8.2/bin/solr zk upconfig -z zoo1:2181 -n vdl -d /opt/configset/vdl_conf/
```

# 2. Create collection with custom schema
```bash
docker exec -it solr1 /opt/solr-8.8.2/bin/solr -c vdl -d /opt/vdl_config -n vdl -shards 2 replicationFactor 2 -p 8981 -V

http://localhost:8981/solr/admin/collections?action=CREATE&name=vdl&numShards=6&replicationFactor=3&maxShardsPerNode=-1&collection.configName=vdl&wt=json
```

# 3. Full Import Database Data
```
http://localhost:8981/solr/dih/dataimport?command=full-import&jdbcurl=<jdbc-url>&jdbcuser=<jdbc-user>&jdbcpassword=<jdbc-password>
```
