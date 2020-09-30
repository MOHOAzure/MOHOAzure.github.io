# Site Reliability Troubleshooting with Cloud Monitoring APM

## Book
[site reliability books](https://landing.google.com/sre/books/)
- Chapter: Service Level Objectives

## Infrastructure setup
- Created a cluster with Google Kubernetes Engine

## Deploy application on the cluster
- Deploy the microservices application called Hipster Shop to the cluster with Skaffold to create an actual workload to monitor.
- [microservices demo](https://github.com/GoogleCloudPlatform/microservices-demo)
- [Skaffold](http://skaffold.dev/)

## Develop Sample SLOs and SLIs
"It's impossible to manage a service correctly, let alone well, without understanding which behaviors really matter for that service and how to measure and evaluate those behaviors. To this end, we would like to define and deliver a given level of service to our users, whether they use an internal API or a public product.

"We use intuition, experience, and an understanding of what users want to define service level indicators (SLIs), objectives (SLOs), and agreements (SLAs). These measurements describe basic properties of metrics that matter, what values we want those metrics to have, and how we'll react if we can't provide the expected service. Ultimately, choosing appropriate metrics helps to drive the right action if something goes wrong, and also gives an SRE team confidence that a service is healthy.

"An SLI is a service level indicator—a carefully defined quantitative measure of some aspect of the level of service that is provided.

"Most services consider request latency — how long it takes to return a response to a request — as a key SLI. Other common SLIs include the error rate, often expressed as a fraction of all requests received, and system throughput, typically measured in requests per second. Another kind of SLI important to SREs is availability, or the fraction of the time that a service is usable. It is often defined in terms of the fraction of well-formed requests that succeed. Durability — the likelihood that data is be retained over a long period of time — is equally important for data storage systems. The measurements are often aggregated: i.e., raw data is collected over a measurement window and then turned into a rate, average, or percentile."

Now that you have established a basic understanding, define the SLIs and SLOs for your application. Given that the application itself serves end user ecommerce traffic, it's going to be very important that user experience remains constant and that performance is good. Monitor SLIs for request latency, error rate, throughput, and availability.

## Service Level Indicators and Objectives
The following SLIs and SLOs are selected based on the end-user experience and the theoretical impact to users and business objectives.
![](https://i.imgur.com/DZNA2Uh.png)


## Front end lentency
- Navigation menu > Monitoring > Alerting
- Add alerting policies
    
## Availability SLI
- Navigation menu > Logging > Create Metric
  - Name: Error Rate SLI
  - Resource type: Kubernetes Container
  - Log level: Error
  - App: current service `label:k8s-pod/app:"currencyservice"`
- Navigation menu > Monitoring > Alerting (Create alert from metric: Error Rate SLI)

## Deploy new release
- measure the impact of application changes on user experience
- modify the Kubernetes manifests for the services which have new releases (change image)


