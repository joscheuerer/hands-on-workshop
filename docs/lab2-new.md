# UseCase 2 - Gitops

## Overview - What's in the section?
Time: ~10 minutes

GitOps is build on the idea that the entire infrastructure and application lifecycle is managed through Git repositories as the single source of truth.
In this section, we are going to work git centric. 

* Configure git triggers in StackGuardian
* Create pull requests in git
* Triggers deployment in SG
* Receive results from deployment, cost calculation and policy evaluation directly in git


## 2.1 - Configure github triggers
### Description
This section shows how to deployments and test can be started from git.
The deployment results, cost calculation and policy evaluation are reported back into git. 

### Setup triggers
Navigate to your existing workflow from the lab before by choosing the **Workflow Groups** in the sidebar. 
Select your your workflow group **wfg-xx**, and then your **repo-vpc-xx**. 
Choose the tab **Settings** and in the section of Git Repository the **Advanced Options**. 
This will bring you to the Button **Configure Github Triggers**. 
Now configure the triggers as shown in the image below. 


### What is the effect of triggers
By setting the triggers the following will happen 
* Each time a pull request towards the tracked branch ('master') is created, the workflow on StackGuardian will run
* The triggered run will deploy the resources (in this case a vpc) in the cloud but will ask for an approval after creating the terraform plan
* A paragraph with comments will be posted in the github pull request to inform the git user about the outcome of the run
