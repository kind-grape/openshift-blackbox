# Openshift-Blackbox

## Setup Blackbox Exporter Docker Pod
Make sure to login to the Openshift Cluster first, and the `oc\kubectl` tool is set against the correct project/namespace 
```
oc new-app docker.io/prom/blackbox-exporter -e DATA_SOURCE_NAME="<username>:<password>@(<service-dns>:3306)/"
```

To be continued.. 
https://github.com/prometheus/blackbox_exporter

Run the docker 
```
docker run --rm -d -p 9115:9115 --name blackbox_exporter -v `pwd`:/config prom/blackbox-exporter:master --config.file=/config/blackbox.yml
```

To check the result for a particular endpoint
```
curl -k http://localhost:9115/probe?target=google.com&module=http_2xx
```