# How to create and use Private Modules

This repository describes how to create a private module within your Terraform Cloud and then how to use this module with Terraform Cloud

This repository is based on this [tutorial](https://learn.hashicorp.com/tutorials/terraform/module-private-registry-share?in=terraform/modules)


# Prerequisites

- You must have a Terraform Cloud account. See [documentation](https://learn.hashicorp.com/tutorials/terraform/cloud-sign-up#create-an-account)  
- A github account
- [OAuth Access](https://www.terraform.io/docs/cloud/vcs/github.html) to Github configured

# How to

## Create a private module within Terraform cloud

1. Fork the below repository to your own environment  
[https://github.com/munnep/terraform-aws-s3-webapp](https://github.com/munnep/terraform-aws-s3-webapp)
2. Keep the name like the following format
```
terraform-<PROVIDER>-<NAME>
```
3. Tag a release to your repository in the following format
Example  
![](media/2021-11-08-11-46-09.png)  
```
1.0.1
```
4. Go to Terraform cloud and login to import the forked module within you registry
5. Go to registry  
![](media/2021-11-08-11-48-36.png)    
6. select publish a module  
![](media/2021-11-08-11-49-01.png)  
7. Connect to your github account  
![](media/2021-11-08-11-49-30.png)    
8. select the repository you just forked and tagged    
![](media/2021-11-08-11-51-14.png)  
9. Publish the module  
![](media/2021-11-08-11-51-34.png)  
10. You should now see your module imported  
![](media/2021-11-08-11-52-01.png)   


## Use the private module

You are now going to actually use the private module you used created. 

1. Fork this repository to your own account  
```
https://github.com/munnep/learn-private-module-root
```
2. in the file ```main.tf``` change the link to your own organization and change the version to the tag release you gave it. 
```
module "s3-webapp" {
  source  = "app.terraform.io/patrickmunne/s3-webapp/aws"
  name        = var.name
  region = var.region
  prefix = var.prefix
  version = "1.0.0"
}

```
3. Go into your Terraform Cloud account
4. Create a new workspace      
![](media/2021-11-08-11-58-15.png)  
5. choose Version Control Workflow  
![](media/2021-11-08-11-58-49.png)  
6. Connect to github  
![](media/2021-11-08-11-59-36.png)  
7. select the repository you forked and altered in this chapter  
![](media/2021-11-08-12-00-14.png)  
8. create the workspace  
![](media/2021-11-08-12-00-42.png)  
9. Go into the workspace and change the variables as below     
![](media/2021-11-08-12-02-15.png)  
10. Start a plan to create it    
![](media/2021-11-08-12-03-09.png)  
11. Confirm and apply the plan  
![](media/2021-11-08-12-06-29.png)  
12. After the apply your resources should be created  
![](media/2021-11-08-12-07-21.png)  
13. Destroy your environment. Go to settings and Destruction and Deletion  
![](media/2021-11-08-12-08-21.png)  
14. Manually destroy   
![](media/2021-11-08-12-08-44.png)  
15. Queue destroy plan  
![](media/2021-11-08-12-09-15.png)  
16. Confirm and apply  
![](media/2021-11-08-12-10-01.png)  