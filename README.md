# Introduction
This learning path helps you contenarize mernstack movie application,that can be used for managing information about movies.




# Steps
 1.Setup a kubernetes cluster with 3 worker nodes using OKE.
   Follow this tutorial :  https://www.oracle.com/webfolder/technetwork/tutorials/obe/oci/oke-full/index.html) 
 
   
   Set up  bashion host with below configuration in the vcn where k8s cluster is present:
   
   Tutorial for launching Compute Instance(https://docs.oracle.com/en-us/iaas/Content/Compute/Tasks/launchinginstance.htm)
   
![bashionhost](https://user-images.githubusercontent.com/77958988/109423858-35266300-7a07-11eb-8d97-8ce990430735.png)

 2.Install oci-cli on bashion host using below commands . 


```
   bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
   oci -v
   oci set config
```   
"oci set config" command will ask for user OCID,tenancy OCID and region.
 user OCID is shown in user profile information and tenancy OCID is shown in tenancy information
 User Profile Information
![userprof](https://user-images.githubusercontent.com/77958988/109422219-a3b3f280-7a00-11eb-96bc-f0a5d988de04.png)

![userp](https://user-images.githubusercontent.com/77958988/109422243-be866700-7a00-11eb-9f41-67c24dc44f77.png)

Tenancy Information

![tenancyinfo](https://user-images.githubusercontent.com/77958988/109422393-58e6aa80-7a01-11eb-911c-a2a34c29d9aa.png)

