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

In the sidebar click on **Deploy** followed by **Worgflowgroup**. Choose **Fresenius-Demo**

<img width="1122" alt="image" src="https://github.com/user-attachments/assets/0d24239d-c772-4ffd-9b58-b9025a7035f1" />


