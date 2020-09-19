# Awwvision: Cloud Vision API from a Kubernetes Cluster
uses Kubernetes and Cloud Vision API to demonstrate how to use the Vision API to classify (label) images from Reddit's /r/aww subreddit and display the labelled results in a web app.

## Create a Kubernetes Engine cluster
* create a cluster in the us-central1-a zone, and start up the cluster
```
gcloud config set compute/zone us-central1-a

gcloud container clusters create awwvision \
    --num-nodes 2 \
    --scopes cloud-platform
```

* use the container's credentials
```
gcloud container clusters get-credentials awwvision
```

* verify that everything is working
```
kubectl cluster-info

Kubernetes master is running at https://35.192.118.247
GLBCDefaultBackend is running at https://35.192.118.247/api/v1/namespaces/kube-system/services/default-http-backend:http/proxy
Heapster is running at https://35.192.118.247/api/v1/namespaces/kube-system/services/heapster/proxy
KubeDNS is running at https://35.192.118.247/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://35.192.118.247/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy
```

## Create a virtual environment, and then active it
```
virtualenv -p python3 venv

source venv/bin/activate
```

## Add sample data to awwvision project, and then build and deploy everything
As part of the process, Docker images will be built and uploaded to the Google Container Registry private container registry. In addition, yaml files will be generated from templates, filled in with information specific to your project, and used to deploy the redis, webapp, and worker Kubernetes resources for the lab.
```
git clone https://github.com/GoogleCloudPlatform/cloud-vision

cd cloud-vision/python/awwvision

make all
```

## Check the Kubernetes resources on the cluster
* list the [pods](https://kubernetes.io/docs/concepts/workloads/pods/pod)
```
kubectl get pods

NAME                                READY   STATUS    RESTARTS   AGE
awwvision-webapp-6d7b596478-x45mg   1/1     Running   1          2m5s
awwvision-worker-6bc84df6b5-gs6zk   1/1     Running   0          62s
awwvision-worker-6bc84df6b5-vjcd9   1/1     Running   0          62s
awwvision-worker-6bc84df6b5-xp4rt   1/1     Running   1          62s
redis-master-7c57dbd-vrk46          1/1     Running   0          3m40s
```

* list the [deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment)
```
kubectl get deployments -o wide

NAME               READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS         IMAGES              SELECTOR
awwvision-webapp   1/1     1            1           3m4s    awwvision-webapp   gcr.io/qwiklabs-gcp-02-10a211872692/awwvision-webapp   app=awwvision,role=frontend
awwvision-worker   3/3     3            3           2m1s    awwvision-worker   gcr.io/qwiklabs-gcp-02-10a211872692/awwvision-worker   app=awwvision,role=worker
redis-master       1/1     1            1           4m39s   redis-master       redis              app=redis,role=master
```

* get the external IP address of the webapp [service](https://kubernetes.io/docs/concepts/services-networking/service)
```
kubectl get svc awwvision-webapp

NAME               TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE
awwvision-webapp   LoadBalancer   10.3.253.157   34.123.144.20   80:31293/TCP   4m35s
```

## Visit the new created web app and start its crawler
* Visit the web app by its IP retrieved by previous step
![](https://i.imgur.com/bDUBCXE.png)
![](https://i.imgur.com/uTE26Mk.png)
