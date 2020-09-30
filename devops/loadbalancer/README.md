# Deploy Kubernetes Load Balancer Service with Terraform
## Why Terraform
  While you could use kubectl or similar CLI-based tools mapped to API calls to manage all Kubernetes resources described in YAML files, orchestration with Terraform presents a few benefits.

  - Use the same configuration language to provision the Kubernetes infrastructure and to deploy applications into it.
  - drift detection: `terraform plan` will always present you the difference between reality at a given time and config you intend to apply.
  - full lifecycle management: Terraform doesn't just initially create resources, but offers a single command to create, update, and delete tracked resources without needing to inspect the API to identify those resources.
  - synchronous feedback: While asynchronous behavior is often useful, sometimes it's counter-productive as the job of identifying operation result (failures or details of created resource) is left to the user. e.g. you don't have IP/hostname of load balancer until it has finished provisioning, hence you can't create any DNS record pointing to it.
  - graph of relationships: Terraform understands relationships between resources which may help in scheduling - e.g. Terraform won't try to create a service in a Kubernetes cluster until the cluster exists.

## Config files of Terraform
 k8s.tf &  main.tf 
  - main.tf 
  
  ```tf
  variable "region" {
    default = "us-west1"
  }

  variable "location" {
    default = "us-west1-b"
  }

  variable "network_name" {
    default = "tf-gke-k8s"
  }

  provider "google" {
    region = var.region
  }

  resource "google_compute_network" "default" {
    name                    = var.network_name
    auto_create_subnetworks = false
  }

  resource "google_compute_subnetwork" "default" {
    name                     = var.network_name
    ip_cidr_range            = "10.127.0.0/20"
    network                  = google_compute_network.default.self_link
    region                   = var.region
    private_ip_google_access = true
  }

  data "google_client_config" "current" {
  }

  data "google_container_engine_versions" "default" {
    location = var.location
  }
  ```
  
  - k8s.tf
  
  ```tf
  provider "kubernetes" {
    version = "~> 1.10.0"
    host    = google_container_cluster.default.endpoint
    token   = data.google_client_config.current.access_token
    client_certificate = base64decode(
      google_container_cluster.default.master_auth[0].client_certificate,
    )
    client_key = base64decode(google_container_cluster.default.master_auth[0].client_key)
    cluster_ca_certificate = base64decode(
      google_container_cluster.default.master_auth[0].cluster_ca_certificate,
    )
  }

  resource "kubernetes_namespace" "staging" {
    metadata {
      name = "staging"
    }
  }

  resource "google_compute_address" "default" {
    name   = var.network_name
    region = var.region
  }

  resource "kubernetes_service" "nginx" {
    metadata {
      namespace = kubernetes_namespace.staging.metadata[0].name
      name      = "nginx"
    }

    spec {
      selector = {
        run = "nginx"
      }

      session_affinity = "ClientIP"

      port {
        protocol    = "TCP"
        port        = 80
        target_port = 80
      }

      type             = "LoadBalancer"
      load_balancer_ip = google_compute_address.default.address
    }
  }

  resource "kubernetes_replication_controller" "nginx" {
    metadata {
      name      = "nginx"
      namespace = kubernetes_namespace.staging.metadata[0].name

      labels = {
        run = "nginx"
      }
    }

    spec {
      selector = {
        run = "nginx"
      }

      template {
        container {
          image = "nginx:latest"
          name  = "nginx"

          resources {
            limits {
              cpu    = "0.5"
              memory = "512Mi"
            }

            requests {
              cpu    = "250m"
              memory = "50Mi"
            }
          }
        }
      }
    }
  }

  output "load-balancer-ip" {
    value = google_compute_address.default.address
  }
  ```

## Initialize and install dependencies
- `terraform init`
  to prepare a working directory for use and is always safe to run multiple times, to bring the working directory up to date with changes in the configuration

- `terraform plan` 
  to see any changes that are required for your infrastructure.
  
- `terraform apply`
  to apply the changes required to reach the desired state of the configuration.
## Infrastructure created with Terraform
  ![](https://i.imgur.com/drkEB51.png)
