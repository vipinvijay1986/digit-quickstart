### Quick setup Of [Digit System] (https://docs.digit.org/urban/platform/setup-digit/quickstart#quickstart-setup)

#### **Step 1: Prerequisite for setup on** (**window system using AWS cloud vm**)  : 
*For installing the package use powershell administrator mode*. 
1. [Chocolatey](https://chocolatey.org/install#individual), [YouTube reference](https://youtu.be/HxU8CcTUnxA)
5. [Git](https://git-scm.com/download/win)
6. Kubectl command : `choco install kubernetes-cli`
7. curl command : `choco install curl`
8. ssh keygen ( ByDefault in window 11 )  command:  `ssh-keygen` 
9. [Terraform](https://releases.hashicorp.com/terraform/0.14.10/)
10. [AWS cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
11. [Golang](https://go.dev/dl/) v1.13.3
12. [Postman](https://www.postman.com/downloads/)



#### **Step 2 : Create AWS User with ec2 permission**  
* To create a user on AWS console follow the [link](https://www.youtube.com/watch?v=_9u5LuL8KmM) . 
* To create AWSprofile (Access key and Secret key needs to be added from previous step): 
```
aws configure --profile digit-quickstart-poc 
AWS Access Key ID []:
AWS Secret Access Key []:
Default region name []: ap-south-1
Default output format []: text
export AWS_PROFILE=digit-quickstart-poc   (linux/mac)
setx AWS_PROFILE digit-quickstart-poc  (window)
```
#### **Step 3 : SSH keyGen, Git Clone**  
```
> ssh-keygen 
> git clone -b quickstart https://github.com/egovernments/DIGIT-DevOps 
```
#### **Step 3b : Terraform execution** 
* Copy the public IP to login to VM.
* Create Cluster and  copy the cluster config file to local system. : 
```
scp -i /c/Users/Vipin/.ssh/id_rsa ubuntu@<VM_PUBLIC_IP>:/home/ubuntu/kube/myk3dconfig ./myk3dconfig
```


#### **Step 4: Deployment of Platform /PGR services** 

Assign the full privilage to kube folder in VM. 
```
ssh -i /D/egov/digit/awsSetup/DIGIT_31072022/id_rsa ubuntu@<VM_PUBLIC_IP>
cd ~
sudo chmod -R 777 kube
kubectl delete pod zookeeper-0 -n zookeeper-cluster --kubeconfig=/home/ubuntu/kube/myk3dconfig
kubectl delete pod kafka-0 -n kafka-cluster --kubeconfig=/home/ubuntu/kube/myk3dconfig
```

#### **Step 5 : Do the port forwarding and run the postman scripts** 

#### **Step 6 : Delete Cluster**  ( Optional , if you want to delete cluster)
```
cd DIGIT-DevOps/infra-as-code/terraform/quickstart-aws-ec2
terraform destroy
```
 


