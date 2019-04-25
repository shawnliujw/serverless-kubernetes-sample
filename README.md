# kubernetes serverless sample
serverless sample  in kubernetes , here will use kubeless and its [serverless plugin](https://serverless.com/framework/docs/providers/kubeless/) 

* the serverless plugin for kubeless now only support the following runtimes
Node.js,Python,Ruby


**Supported Runtimes**  
`ballerina0.981.0, dotnetcore2.0, dotnetcore2.1, go1.10, java1.8, nodejs6, nodejs8, php7.2, python2.7, python3.4, python3.6, python3.7, ruby2.3, ruby2.4, ruby2.5, jvm1.8, nodejs_distroless8, nodejsCE8, vertx1.8`

##Preparation  
* Ensure you have available kubernetes cluster . See [Setup Kubernetes By Kubeadm](https://github.com/shawnliujw/spring-boot-kubernetes/blob/master/kubeadm/setup.md) if you don't have.  
* Install serverless, see the [guide](https://serverless.com/framework/docs/getting-started/)
##Install Kubeless  
```bash
export RELEASE=$(curl -s https://api.github.com/repos/kubeless/kubeless/releases/latest | grep tag_name | cut -d '"' -f 4)
export OS=$(uname -s| tr '[:upper:]' '[:lower:]')

curl -OL https://github.com/kubeless/kubeless/releases/download/$RELEASE/kubeless_$OS-amd64.zip && \
unzip kubeless_$OS-amd64.zip && \
sudo mv bundles/kubeless_$OS-amd64/kubeless /usr/local/bin/
```  
##Setup  
```bash
kubectl create ns kubeless
kubectl create -f https://github.com/kubeless/kubeless/releases/download/$RELEASE/kubeless-non-rbac-$RELEASE.yaml
kubectl get pods -n kubeless
kubectl get deployment -n kubeless
kubectl get customresourcedefinition
```  
See More [Here](https://kubeless.io/docs/quick-start/)
##Test  

**Java**  
* `cd java/ && sh deploy.sh`  
* Check the deployment status executing `kubeless function ls hello-java`
wait a few seconds for the 

**Nodejs**
* `cd nodejs && sls deploy`
*  run `sls invoke --function hello-nodejs` to check the response  

**Python**  

* `cd python && sls deploy`
*  run `sls invoke --function hello-python` to check the response