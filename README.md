# AWS EKS Service Mesh using App Mesh

*This repository contains Terraform scripts and Kubernetes configuration files for setting up secure microservices communication using AWS App Mesh on an Amazon EKS cluster.*

## Overview

AWS App Mesh is a service mesh that provides application-level networking, making it easy for services to communicate across different types of compute infrastructure. AWS App Mesh standardizes how services communicate, providing end-to-end visibility and ensuring high-availability.

The Terraform script sets up an EKS cluster and node group, while the Kubernetes configurations set up the App Mesh controller and define the services.

AWS App Mesh uses Envoy as its data plane, and each microservice should have an Envoy sidecar.

## Prerequisites

1. [AWS CLI](https://aws.amazon.com/cli/)
2. [Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)
3. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
4. [Helm](https://helm.sh/docs/intro/install/)
5. [IAM Authenticator for AWS](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)

## Getting Started

1. **Clone the repository**:

```
git clone https://github.com/<your-repo>/aws-eks-app-mesh.git
cd aws-eks-app-mesh
```

2. **Apply the Terraform scripts:**

``````
cd terraform
terraform init
terraform plan
terraform apply
``````

3. **Install the AWS App Mesh controller on your EKS cluster:**

``````
helm repo add eks https://aws.github.io/eks-charts
helm upgrade -i appmesh-controller eks/appmesh-controller --namespace appmesh-system
``````
4. **Apply the Kubernetes configurations:**

``````
kubectl apply -f kubernetes/
``````

## Monitoring

*AWS App Mesh integrates with AWS CloudWatch and AWS X-Ray for comprehensive observability. They provide insights into latency, HTTP headers, methods, URLs, and success rates.*

**AWS CloudWatch**: Navigate to AWS CloudWatch in your AWS console to monitor your service metrics.

**AWS X-Ray:** Navigate to AWS X-Ray in your AWS console for a detailed view of the requests traveling through your application.

**Cleanup**

To cleanup the resources created by Terraform:

```terraform destroy```

To delete the Kubernetes deployments:


```kubectl delete -f kubernetes/```


---

*Note: This is a basic README file and can be improved based on the specific requirements of the project. Be sure to add any additional steps or details necessary based on your implementation.*
