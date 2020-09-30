# Continuous Delivery with Jenkins

## Continuous Delivery / Continuous Deployment
When you need to set up a continuous delivery (CD) pipeline, deploying Jenkins on Kubernetes Engine provides important benefits over a standard VM-based deployment.
When your build process uses containers, one virtual host can run jobs on multiple operating systems. Kubernetes Engine provides ephemeral build executors—these are only utilized when builds are actively running, which leaves resources for other cluster tasks such as batch processing jobs. Another benefit of ephemeral build executors is speed—they launch in a matter of seconds.
Kubernetes Engine also comes pre-equipped with Google's global load balancer, which you can use to automate web traffic routing to your instance(s). The load balancer handles SSL termination and utilizes a global IP address that's configured with Google's backbone network—coupled with your web front, this load balancer will always set your users on the fastest possible path to an application instance.
Now that you've learned a little bit about Kubernetes, Jenkins, and how the two interact in a CD pipeline, it's time to go build one.

## Jenkins
[Jenkins](https://jenkins.io/) is an open-source automation server that lets you flexibly orchestrate your build, test, and deployment pipelines. Jenkins allows developers to iterate quickly on projects without worrying about overhead issues that can stem from continuous delivery.

## Lab Sample
https://github.com/GoogleCloudPlatform/continuous-deployment-on-kubernetes.git

## Create clusters

```
gcloud container clusters create jenkins-cd \
--num-nodes 2 \
--machine-type n1-standard-2 \
--scopes "https://www.googleapis.com/auth/source.read_write,cloud-platform"
```

##  Get the credentials for your cluster
Kubernetes Engine uses these credentials to access the newly provisioned cluster
`gcloud container clusters get-credentials jenkins-cd`

## Install Helm and grant Tiller (the server side of Helm)
In this lab, you will use Helm to install Jenkins from the Charts repository. Helm is a package manager that makes it easy to configure and deploy Kubernetes applications. Once you have Jenkins installed, you'll be able to set up your CI/CD pipeline.
```
wget https://storage.googleapis.com/kubernetes-helm/helm-v2.14.1-linux-amd64.tar.gz

tar zxfv helm-v2.14.1-linux-amd64.tar.gz
cp linux-amd64/helm .

kubectl create clusterrolebinding cluster-admin-binding --clusterrole=cluster-admin --user=$(gcloud config get-value account)

kubectl create serviceaccount tiller --namespace kube-system
kubectl create clusterrolebinding tiller-admin-binding --clusterrole=cluster-admin --serviceaccount=kube-system:tiller

./helm init --service-account=tiller
./helm update
```

## Configure and Install Jenkins
Use the Helm CLI to deploy the chart with your configuration settings.
```
./helm install -n cd stable/jenkins -f jenkins/values.yaml --version 1.2.2 --wait
```

## Connect to Jenkins
- Retrieve pw created by Jenkins chart
  ```
  printf $(kubectl get secret cd-jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo
  ```
  
- Open Jenkins page with admin/[PW]

## Deploying the Application
Deploy the application into two different environments:
- Production: The live site that your users access.
- Canary: A smaller-capacity site that receives only a percentage of your user traffic. Use this environment to validate your software with live traffic before it's released to all of your users.

## Scale up replicas
- 5 pods (4 replicas) for frontend
  - 1 for canary
  - 4 for production
 - 2 pods for the backend
  - 1 for production
  - 1 for canary
  
## Creating the Jenkins Pipeline
- Prepare dev repo, e.g., a github repo
- In Jenkins page
  - create service account credentials
  - create a Jenkins job
    A job named Branch indexing runs. This meta-job identifies the branches in your repository and ensures changes haven't occurred in existing branches
    
    
## Creating the Development Environment
After modifying the master repo, Jenkins would try to build the project. Check out the main page of Jenkins for CD.
