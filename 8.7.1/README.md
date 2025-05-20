# Setup Elastic APM

Original docker compose file from https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

I have changed the places with `#NEW` comment.

# APM Plugin

Reference on how to plug APM into the elastic stack https://stackoverflow.com/a/75765245/393046

I decided that the APM server shouldn't know the Kibana server, so I removed from the `apm` service the following configurations:

```
-E setup.kibana.host=kibana:5601
-E apm-server.kibana.enabled=true
-E apm-server.kibana.host=kibana:5601
-E apm-server.kibana.protocol=https
-E apm-server.kibana.username=kibana_system
-E apm-server.kibana.password=${KIBANA_PASSWORD}
-E apm-server.kibana.ssl.certificate_authorities=config/certs/ca/ca.crt
-E apm-server.kibana.ssl.verification_mode=none
```
