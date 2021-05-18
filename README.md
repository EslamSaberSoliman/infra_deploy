#### This is a Repository for implement the infrastructure via terraform and Jenkins Pipeline.

#### To use this repo, You need to check the pre-request first as below:

1. I use here jenkins as CI/CD Tool, so you need to have jenkins to run this pipeline. Jenkins server should support Terraform. You can use the below to create jenkins sever that support Terraform:

```
#create docker image
FROM  jenkins/jenkins:lts
USER root
RUN apt-get update && apt-get install -y gnupg software-properties-common curl && curl -fsSL https://apt.releases.hashicorp.com/gpg | apt-key add -
RUN apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main" && apt-get update && apt-get install -y terraform
USER jenkins

```

```
#run jenkins in a container
docker run --name jenkins -p 8080:8080 -p 50000:50000 --restart=always \
  -v $(pwd)/jenkins_home:/var/jenkins_home \
  jenkins-docker
```

2. You should add your Github  credential and AWS credential in jenkins via manage credential.






### After you finished the pre-request, You able to use this repo by adding jenkinsfile in this repo with your credentials that you set in pre-request step in the environment section in this file. After that you can create your pipeline using this jenkinsfile and use it create or destroy your environment



### Also after creating your infrastructure, you can use this repo to install prometheus/grafana as monitor tool
## Via helm 

```
helm install prom-grafana prom-grafana-via-helm
```

## Via kubectl

```
kubectl apply -k prom-grafana-via-kubectl-apply
```
