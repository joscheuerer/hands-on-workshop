# Usecase 2 - Templates and NoCode

## Overview - What's in the section?
Time: ~30 minutes

In this section, we will begin to make use of the StackGuardian marketplace, which can be seen as a library for templates and blueprints. But it is more than that - it also allows you to manage the version and lifecycle of your IaC templates, across different protocols (like Terraform, Ansible Playbooks, Helm Charts etc..), combine multiple templates/protocols into a stack and use NoCode to deploy them. 
The goal of this use-case is to demonstrate the following:

* Standardize on blueprints and templates
* Collaborate between teams in an organisation
* NoCode Interface to simplify deployment of infrastructure
* Versioning and lifecycle of templates


![Usecase 2](image/usecase2.png)
_Fig. Use the marketplace to manage and deploy templates_

## 2.1 - Create template in marketplace
### Description
In this lab you will see how quickly a new template in the private marketplace can be created.


### Create template in marketplace
On the left top click on the 9 dots next to Orchestrator and then on **Marketplace**
  
![Marketplacelink](image/marketplacelink.png)  
_Fig. Marketplace Link_  
  
Once on the marketplace you can try out the different links and then continue to **Create Template +** which you can find on the top right hand side of the screen.

![Create Template](image/marketplace.png) 
_Fig. Create template on marketplace_  

1. Template Name = ``vpc-xx``
2. Scroll down and set Source Config Kind = **TERRAFORM**
3. Source Destination Kind = **github.com**
4. Repository URL = ``https://github.com/StackGuardian/terraform-aws-vpc``
5. On the bottom right of the screen click **Generate No Code Form**
6. By scrolling down you see the variables that were identified in the IaC and loaded into the template.
7. Hit **Create** to add this template to your marketplace.

Later on the instructor will go through the different tabs with the whole group but you can also explore the tabs Usage, Analysis, Code, Meta already now. 
Btw. the **NoCode** tab is used to adjust the generated NoCode interface.


## 2.2 - Deploy an AWS VPC from existing template via NoCode
### Description
In this exercise you will **NOT** use the previously created template. 
Rather we put you in the shoes of a Cloud Consumer or Developer, who is not too much into IaC syntax. The NoCode interfaces allows also non-IaC-experts to use IaC.

### Deploy infrastructure from template
Change back into the orchestrator and click on **Workflow Groups** in the menubar. 

1. Choose your workflow group **wfg-xx**.
2. On the right top you can find **Create Workflow >> Use Wizard >> Terraform**
3. Source Options = ``Marketplace``
4. Browse Templates = **vpc**
5.  The following form should read the following entries
    * Workflow Type = terraform
    * For Source Options choose ``VCS Provider``
    * VCS Configuration is ``Github``
    * Provider/Repository Path = ``https://github.com`` / ``StackGuardian/terraform-aws-vpc`` 
    * The rest leave unchanged 
    * Hit **Save**


1. Select Workflow Group = **wfg-xx**
2. Click **Next**
---
3. Workflow Name = **marketplace-vpc-xx**
4. Click **Next**
---
5. Choose Connector = **AWS-Deploy-Role**
6. Click **Next**
---
7. Scroll down and set the textfield: VPC Name = **workshop-vpc-xx**
8. CIDR Block for VPC = _choose one_
9. Public Subnets IP Addresses = _choose one_
10. Private Subnets IP Addresses = _choose one_
11. Click **Save**
---

You created a workflow from a template in the marketplace, but the resources are not yet deployed yet. 

To do so, click the **Play-button** on the top left and afterwards **Run Workflow** in the flyout. 

![VPC revision](image/playbutton.png) 

_Fig. Deploy resources via Play-button and Run workflow_ 



In the **Runs** tab you can now follow the deployment. Once the VPC is ready, the Status will change to **Completed**. 

The instructor will show the different capabilities in the marketplace. If you have a usecase in mind, feel free to ask how this can be done in StackGuardian.
