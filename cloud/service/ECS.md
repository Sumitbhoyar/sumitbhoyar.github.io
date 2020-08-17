# Amazon Elastic Container Service

Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service. Customers such as Duolingo, Samsung, GE, and Cookpad use ECS to run their most sensitive and mission critical applications because of its security, reliability, and scalability.

ECS is a great choice to run containers for several reasons. First, you can choose to run your ECS clusters using  [AWS Fargate](https://aws.amazon.com/fargate/), which is serverless compute for containers. Fargate removes the need to provision and manage servers, lets you specify and pay for resources per application, and improves security through application isolation by design.

## How Amazon ECS works
![How Amazon ECS works](https://d1.awsstatic.com/diagrams/product-page-diagrams/product-page-diagram_ECS_1.86ebd8c223ec8b55aa1903c423fbe4e672f3daf7.png)
## Use cases
#### Hybrid Deployment

You can use ECS on Outposts to run containerized applications that require particularly low latencies to on-premises systems. AWS Outposts is a fully managed service that extends AWS infrastructure, AWS services, APIs, and tools to virtually any connected site. With ECS on Outposts, you can manage containers on-premises with the same ease as you manage your containers in the cloud.  

#### Machine Learning

You can use AWS Deep Learning Containers for training and serving models in TensorFlow, PyTorch, and MXNet on ECS. You can also accelerate deep learning inference workloads in ECS by using  [Amazon Elastic Inference (EI)](https://aws.amazon.com/machine-learning/elastic-inference/).  

#### Batch Processing

You can run sequential or parallel batch workloads on ECS using AWS Batch. AWS Batch enables you to easily and efficiently run hundreds of thousands of batch computing jobs by dynamically provisioning the optimal quantity and type of compute resources based on the volume and specific resource requirements of the batch jobs submitted.  

#### Web Applications

You can build web applications that automatically scale up and down and run in a highly available configuration across multiple Availability Zones. By running on ECS, your web applications benefit from the performance, scale, reliability, and availability of the AWS. Additionally, your services get out-of-the-box integrations with AWS networking and security services, such as Application Load Balancers for load distribution of your web application and VPC for networking.