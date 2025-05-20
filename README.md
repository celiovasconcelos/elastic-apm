# elastic-apm

Elastic APM Docker Compose on Oracle Linux hosted in Oracle Cloud.

## 1 - Git install

`sudo yum install git`

## 2 - Docker install

Install docker https://docs.docker.com/engine/install/rhel/

```
sysctl vm.max_map_count
echo "vm.max_map_count = 262144" | sudo tee /etc/sysctl.d/99-vm-max-map-count.conf
sudo sysctl --system
```

## 3 - Setup

1. `git clone https://github.com/celiovasconcelos/elastic-apm.git`
2. `vim elastic-apm/8.7.1/.env` (change those 3 passwords)
3. `vim elastic-apm/8.7.1/kibana.yaml` (change those 2 keys and the publicBaseUrl)
4. Allow Source CIDR: 0.0.0.0/0 in Ingress Rules for Default Security List for 443 and 8200 in the Oracle Cloud Console.

## 4 - Run

```
cd elastic-apm/8.7.1/
sudo docker compose up -d
```

## Java agent sample

```
java -javaagent:elastic-apm-agent-1.38.0.jar \
'-Delastic.apm.service_name=sppws' \
'-Delastic.apm.secret_token=*******' \
'-Delastic.apm.verify_server_cert=false' \
'-Delastic.apm.server_url=https://localhost:8200' \
'-Delastic.apm.environment=development' \
'-Delastic.apm.application_packages=br.gov.go' \
-jar .\target\myapp-1.0.0.jar
```
