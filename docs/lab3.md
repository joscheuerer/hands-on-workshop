# Usecase 3 - Build Architecture

## Overview - What's in the section?
Time: ~30 minutes  

In this part of the workshop, we are going to show the power of combining multiple templates and protocols into one infrastructure stack. This allows us to build complex architectures and make them available across departments to the whole organisation. No need to reinvent the wheel over and over again. 
To summarise we want to achieve the following:

* Build production-grade architecture
* Combine multiple protocols in a IaC Group
* Deploy the infrastructure stack with NoCode interface
* Self-service for developers and business lines

![Usecase 3](image/usecase3.png)
_Fig. Build Architectures in StackGuardian_

## 3.1 - Closer Look at the EKS cluster IaC Group
### Description
Until now we were only dealing with low level templates which are VPCs, VMs, Storage Accounts, Resource Groups .... Now we are arranging them into production-grade building-blocks that allows organisations to standardize their deployments. 

### EKS-Cluster
In the marketplace we will use the predefined IaC Group for EKS-Cluster. Go to the marketplace, choose **workshop Templates** and **IAC Groups** on the left. Then select the **aws-eks-cluster** IaC Group. 

![IaC Group](image/iac-group.png)  
_Fig. IaC Groups in the StackGuardian Marketplace_   

In the tab **Templates** you can see, that this IaC Group consists of three templates: 
* EKS Cluster - Terraform
* EKS Cluster Nodes - Terraform
* NginX Service - Helm Chart

Later, with the instructor we will look more in detail, how the single templates are connected to each other and paramaters are passed from one template to the next.

## 3.2 - Deploy the EKS cluster 
### Description
In this exercise we will deploy a cluster from the prespective of a cloud consumer that is not regularly using IaC. 
We will use the previously created VPC (section 2.2) and deploy the EKS Cluster building-block into it. 


### EKS-Cluster with Node and Webserver
Go into the orchestrator and choose your Workflowgroup **wfg-xx**.
Click the tab **Stacks** and afterwards **Create Stack**.

1. Enter the Resource Name = ``eks-xx`` (xx being your number)
2. Under IAC Group Configuration choose the **/workshop/aws-eks-cluster** and the latest revision
3. Hit **Next**
---
4. Most of the configuration like runner constraint (shared) and in which account the resources will get deployed into (connector), is already pre-populated in this eks building-block. Scroll down and enter 
   Cluster Name = ``eks-xx`` (xx being your number) 
5. Cluster Version = ``1.25``
6. Subnet IDs for Cluster 
    * **Click the little wheel on the right side, next to the textbox**
    * Workflow Group Name = **wfg-xx**
    * Stack Name = _leave empty_
    * Workflow Name = **marketplace-vpc-xx**
    * Output Key = ``public_subnets.value``
    * Click **OK**

![Subnet IDs](image/public-subnets.png)
_Fig. Subnet IDs for Cluster_

7. Default Security Group ID
    * **Click little wheel on the right side, next to the textbox**
    * Workflow Group Name = **wfg-xx**
    * Stack Name = _leave empty_
    * Workflow Name = **marketplace-vpc-xx**
    * Output Key = ``default_security_group_id.value``
    * Click **OK**

![Default Security Group ID ](image/security-group.png)
_Fig. Default Security Group ID_

8. Click **Next**
---

9. Name of Managed Node Group = ``eks-managed-node-xx`` 
10. Subnet IDs for Cluster Nodes
    * **Click little wheel next to the textbox**
    * Workflow Group Name = **wfg-xx**
    * Stack Name = _leave empty_
    * Workflow Name = **marketplace-vpc-xx**
    * Output Key = ``public_subnets.value``
    * Click **OK**

![Subnet IDs](image/public-subnets.png)
_Fig. Subnet IDs for Cluster Nodes_


11. Click **Next**
---

**The K8S_CLUSTER_NAME under Environmental Variables will be pulled from the previous template and is already prefilled**

12. Click **Next**
---

13. Use **Create and Execute Workflows**
14. **Go to created stack**

Well done! After a few seconds (use refresh button) the first workflow will start running and deploys the first template - the EKS cluster. 
A stack automatically chains the workflows with each other, that means when one workflow finishes, it kicks off the next one in row until the whole stack is deployed. 

![Stack Deploy](image/stack-deploy.png)
_Fig. Stack of EKS Cluster being deployed_


**It is time to lay back and let StackGuardian do the work.**
The deployment will take about 15min. Time enough to check out the workflows and what is getting created.
