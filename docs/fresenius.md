# Usecases Fresenius

## Overview - What's in the section?
Time: ~15 minutes  

In this workshop you will run the following usecases:

* Deploy production-grade infrastrcuture
* Update deployed infrastructure
* Destroy existing infrastructure
  
## 4.1 - Deploy environment with webserver in Azure

In the sidebar click on **Dev Portal**. This will bring you to the Developer Portal, which allows anybody in the organisation to deploy infrastructure & applications. 

1. In the **Template Type** dropdown choose **IAC Groups**
2. **Use** the **azure-vnet-vm-webserver**

---

3. Workflow Group Name: **Fresenius-Demo** 
4. Stack Name: **Webserver-xx**. xx is the placeholder for the Pod-number you received
Click **Next**.

---

5. Name of Resourcegroup: **rg-xx** (xx is your assigned number)
6. Azure Region to deploy to: **Germany West Central**
7. Vnet Name: **vnet-xx**
8. Name of VM: **vm-xx**
9. Size of VM: **Small (2core)**

Click **Next**.

---
  
6. In Deployment Environment enter the **Connector: AWS-Deploy-Role**
7. Hit **Launch**

---



Well done! This is all that is necessary to deploy the whole building-block. After a few seconds (use refresh button) the first workflow will start running and deploys the first workflow - the VPC. 
A stack automatically chains the workflows with each other, that means when one workflow finishes, it kicks off the next one until the whole stack is deployed. 

![Stack Deploy](image/full-stack-deploy.png)
_Fig. Full-Stack being deployed_

**Now let StackGuardian do the work. The deployment will take about 15min**
In the mean time, check out lab 4.2 and look behind the curtain.


## 4.2 - Closer Look at the Full-Stack IaC Group
### Description
Now we have seen, how simple it can be for the end-user to deploy infrastructure in Self-Service. 
But how are all the single modules/templates connected? How are variables transfered between Terraform and Helm? 

### Full-Stack in Library
Go to the library, choose **Template Type: IAC Groups**. Then select the **aws-full-stack** IaC Group. 

![IaC Group](image/aws-full-stack.png)  
_Fig. IaC Group in the StackGuardian Library_   

In the tab **Templates** you can see, that this IaC Group consists of four templates: 
* VPC Network - Terraform
* EKS Cluster - Terraform
* EKS Cluster Nodes - Terraform
* NginX Service - Helm Chart

You can already have a look at the **View Template Defaults** in each of the templates. 
The instructor we will also take a closer look at the teampletes with the whole group. 
