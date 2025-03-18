# Usecases Fresenius

## Overview - What's in the section?
Time: ~15 minutes  

In this workshop you will run the following usecases:

* Deploy production-grade infrastrcuture
* Update deployed infrastructure
* Destroy existing infrastructure
  
## 4.1 - Deploy build-block with webserver in Azure

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
  
10. In Deployment Environment enter the **Connector: Azure-Deploy**
11. Hit **Launch**

---

Well done! This is all that is necessary to deploy the whole building-block. 

**Now let StackGuardian do the work. The deployment whole will take about 5min**


## 4.2 - Update deployed VM

In the sidebar click on **Deploy** followed by **Workflowgroup**. Choose **Fresenius-Demo** and then select the Tab **Stacks**.

<img width="1122" alt="image" src="https://github.com/user-attachments/assets/0d24239d-c772-4ffd-9b58-b9025a7035f1" />

Here you find all the deployments of the webserver from you and all the other participants of the workshop. Click your **webserver-xx** (xx is your assigned number). In the top right corner you can open **Run Stack** and choose **Modify and Run**. 

<img width="306" alt="image" src="https://github.com/user-attachments/assets/01018cdd-01d7-4ed6-b306-0138275242e2" />

1. Click **Next**

---

2. Change the size of the VM from Small (2core) to **Medium (4core)**.
3. **Next**

---

4. Click **Run**

The changes will be applied to the infrastructureand increasing the size of the VM. 


## 4.3 - Destroy the whole environment including VM

Currently you should be inside of your deployed Stack where it looks like this: 

<img width="1383" alt="image" src="https://github.com/user-attachments/assets/217e04f5-b7e9-4ec2-ae72-e5466b17da0d" />

To destroy the environment you just need to to click **Run Stack** and **Destroy**. This will remove all the resources on Azure in reverse order. Please go ahead and do that. 
