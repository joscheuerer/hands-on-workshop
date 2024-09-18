# Usecase 4 - Build Architecture

## Overview - What's in the section?
Time: ~15 minutes  

In this part of the workshop, we are going to show the power of combining multiple templates and protocols into one infrastructure stack. This allows us to build complex architectures and make them available across departments to the whole organisation. No need to reinvent the wheel over and over again. 
To summarise we want to achieve the following:

* Build production-grade architecture
* Combine multiple protocols in a IaC Group
* Deploy the infrastructure stack with NoCode interface
* Self-service for developers and cloud consumers

![Usecase 4](image/usecase3.png)
_Fig. Build Architectures in StackGuardian_

## 4.1 - Closer Look at the Full-Stack IaC Group
### Description
Until now we were only dealing with low level templates which are VPCs, VMs, Storage Accounts, Resource Groups .... Now we are arranging them into production-grade building-blocks, which allows organisations to standardize their deployments. 

### Full-Stack in Library
In the marketplace we will use the predefined IaC Group that creates a VPC, EKS-Cluster, Worker-nodes and a webserver. Go to the library, choose **Template Type: IAC Groups**. Then select the **aws-full-stack** IaC Group. 

![IaC Group](image/aws-full-stack.png)  
_Fig. IaC Group in the StackGuardian Library_   

In the tab **Templates** you can see, that this IaC Group consists of four templates: 
* VPC Network - Terraform
* EKS Cluster - Terraform
* EKS Cluster Nodes - Terraform
* NginX Service - Helm Chart

This should give you a good idea, what you are going to deploy in the next step. Together with the instructor you will take a closer look later on, to understand how the single templates are connected to each other and paramaters are passed from one template to the next.

## 4.2 - Deploy the Full-Stack 
### Description
In this exercise we will deploy the stack from the prespective of a cloud consumer, who is not familiar with IaC.

### VPC, EKS-Cluster with Node and Webserver
Go back to the library but this time click **Use** in the tile of the full-stack-template.
![IaC Group](image/use-aws-full-stack.png)  
 _Fig. Use aws-full-stack_   

---
In the new Pop-out choose your own 
1. Existing WorkflowGroup: **wfg-xx** and provide as 
2. Stack Name ``full-stack-xx``. 
Click **Next**.

---
In the new Window choose the following options:

3. Enable **Basic Mode**
4. Then scroll to the bottom and hit **Next**

---
5. Meta is already correctly populated with the correct runner info - but you can have a look.
6. In Target Platform Configuration enter the **Connector: AWS-Deploy-Role**
7. In Template Variable Settings insert:
   * VPC name: **vpc-xx**
   * Region: **Frankfurt**
   * Cluster Name: **cluster-xx**
   * Cluster Version: **1.29**
8. Hit **Next**

---

9. Use **Create and Execute Workflows**

Well done! This is all that is necessary to deploy the whole building-block. After a few seconds (use refresh button) the first workflow will start running and deploys the first workflow - the VPC. 
A stack automatically chains the workflows with each other, that means when one workflow finishes, it kicks off the next one until the whole stack is deployed. 

![Stack Deploy](image/full-stack-deploy.png)
_Fig. Full-Stack being deployed_


**It is time to lay back and let StackGuardian do the work.**
The deployment will take about 15min. Time enough to check out the workflows and what is getting created.
