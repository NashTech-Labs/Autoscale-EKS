# Amazon Elastic Kubernetes Service (Amazon EKS)
Its a simple command-line utility for generating and maintaining Kubernetes clusters on Amazon EKS. At the end of this tutorial, you will have a working Amazon EKS cluster that you can deploy applications.

An Amazon EKS cluster consists of two primary components:

The Amazon EKS control plane.
Amazon EKS nodes that are enrolled with the control plane.
Before starting, you must install and configure the following materials for Amazon EKS cluster.

kubectl – A command-line tool for working with Kubernetes clusters.

eksctl – A command-line tool for working with EKS clusters that automates many individual tasks. 

# Prerequisites
Before deploying the Cluster Autoscaler, you must meet the following prerequisites:

Have an existing Amazon EKS cluster – If you don’t have a cluster.
An existing IAM OIDC provider for your cluster. To conclude whether you hold one or need to create one.
Node groups with Auto Scaling groups tags – The Cluster Autoscaler requires the following tags on your Auto Scaling groups so that they can be auto-discovered.

### Let’s create the cluster using this command and usually take about 15-20 minutes to create the cluster.

eksctl create cluster -f eks.yaml

### So, the cluster is ready so to verify the connection, we can use this command:

kubectl get svc

Let’s go-to-the first AWS Management Console and click on the EKS. Select the cluster, As you can see this is our cluster name the eks-name cluster and the version.

And we will go to the EC2 Dashboard and searching for Auto Scalling Groups, you are going to find two Auto Scaling Groups, the first one is for managed nodes and the second one for unmanaged nodes.

### Click on Add Providers.

And click add provider then it’s going to be the open id connect, let’s paste our url and get thumbprint.

And for the audience let’s paste the default value sts.amazonaws.com and let’s create this provider.

Now let’s deploy the Auto Scaler let’s create the folder K8s. We will create the first file for the Auto scaler with name cluster-autoscaler.yaml. The first we are going to create the service account. We are going to add this annotation and replace with this ARN of the role.

You can find a lot of useful logs and if you want to debug to useful read all of the output. And the next step is watch will just repeat this command every two seconds.

 watch kubectl get pods 

watch kubectl get nodes

So Autoscaler is able to set appropriate desired state, desired capacity for each instance groups and you can see that here the min and max=10 and desired capacity=1. So Auto scaler cannot only increase the number of instances it also decrease the number of instances.

And at last if you want to delete your cluster you can use this below command

eksctl delete cluster -f eks.yaml 
