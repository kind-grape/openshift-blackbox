# Openshift-Blackbox

## Setup Blackbox Exporter Docker Pod
Make sure to login to the Openshift Cluster first, and the `oc\kubectl` tool is set against the correct project/namespace 
```
oc new-app docker.io/prom/blackbox-exporter -e DATA_SOURCE_NAME="<username>:<password>@(<service-dns>:3306)/"
```

To be continued.. 
https://github.com/prometheus/blackbox_exporter




- Pull the docker prometheus blackbox exporter image from public repo 
  ```
  docker pull prom/blackbox-exporter
  ```
- Tag the image 
  ```
  docker tag prom/blackbox-exporter registry.ford.com/rpeng14/prom
  ```
- log in to the openshift private registry
  ```
  docker login registry.ford.com
  ```
- Create the image repo in the target private registry and organization
- push the image to the private registry 
  ```
  docker push registry.ford.com/rpeng14/prom/blackbox-exporter
  ```

Once the image tag has been pushed, modify the deployment helm values as shown in the repo 

Deploy the helm chart with the custom values 
```
helm install blackbox-test prometheus-community/prometheus-blackbox-exporter -f .\blackbox-values.yaml
```