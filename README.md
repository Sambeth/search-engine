# Search-Engine

# General set up
1. Create a `security.json` file in the PWD with the following details
```
{
    "authentication":{
       "blockUnknown": true,
       "class":"solr.BasicAuthPlugin",
       "credentials":{"solr":"IV0EHq1OnNrj6gvRCwvFwTrZ1+z1oBbnQdiVC3otuq0= Ndd7LKvVBAaZIF0QAVi1ekCfAJXr1GGfLtRUXhgrF8c="},
       "real": "My Solr Users",
       "forwardCredentials": false
    },
    "authorization":{
       "class":"solr.RuleBasedAuthorizationPlugin",
       "permissions":[{"name":"security-edit",
          "role":"admin"}],
       "user-role":{"solr":"admin"}
    }
}
```
NOTE: This is only for test and development purposes. The preferred method of authentication in production is to enable ssl

2. Run docker compose
```
docker compose up --build -d
```


# Set basic authentication and authorization
```bash
docker exec -it solr1 /opt/solr-8.8.2/bin/solr zk cp file:/opt/solr-8.8.2/server/solr/security.json zk:/security.json -z zoo1:2181
```