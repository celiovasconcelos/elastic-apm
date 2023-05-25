# Setup Elastic APM

Arquivo compose obtido em https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

Os locais de alteração estão marcados com a tag `#NOVO`

# Plugando o APM

Para plugar o APM no Elastic foi usado https://stackoverflow.com/a/75765245/393046

No meu setup descidi que o APM não deve conhece o KIBANA, logo foram **retiradas** do serviço `apm` as seguintes configurações:

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

# Comnado do agente

```
java -javaagent:elastic-apm-agent-1.38.0.jar '-Delastic.apm.service_name=sppws' '-Delastic.apm.secret_token=' '-Delastic.apm.verify_server_cert=false' '-Delastic.apm.server_url=https://localhost:8200' '-Delastic.apm.environment=desenvolvimento' '-Delastic.apm.application_packages=br.gov.go' -jar .\target\infra-1.0.0.jar
```
