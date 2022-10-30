# asnible-terraform
This Repo is for deploying resources using Ansible and Terraform


# Setup notes

Install Terraform and Ansible on the server you want to run the commands.

```
1. Please run the playbook "gen_ssh_key.yaml" , "ansible-playbook ansible_templates/gen_ssh_key.yaml" 
   to generate SSH keypair(on local system) used in TF templates and Ansible for connecting to 
   remote EC2 instances.
   
2. If you still want to initialize directory via "terraform init", then use the "-backend=false" flag,
   like so "terraform init -backend=false"
```

# Deploying Jenkins Master and Worker Nodes in AWS Behind an ALB Using Terraform and Ansible

## Introduction
In this hands-on lab, the student will deploy Jenkins master and worker nodes on AWS EC2 instances across regions through Terraform and manage the software and integration with Ansible.

## Solution
### Log in to the Terraform Controller Node EC2 Instance
Find the details for logging in to the Terraform Controller node provided by the hands-on lab interface and log in to the node using SSH:
```
ssh cloud_user@<IP-OF-TERRAFORM-CONTROLLER>
```
Note: This instance already has an EC2 instance profile (role) attached to it and has all necessary AWS API permissions required for this lab. It also has the AWS CLI set up and configured with the AWS account attached to this lab, for which the console login credentials are also provided in the lab interface page once the lab spins up.

After logging in, verify the version of Terraform installed (should be 12.13). Execute the following command to check:
```
terraform version
```
###
Clone the GitHub Repo for Terraform Code
Use the git command to clone the GitHub repo which has the Terraform code for deploying the solution of this lab. GitHub repo URL.

1. Execute the following command:
```
git clone https://github.com/ACloudGuru-Resources/content-deploying-to-aws-ansible-terraform.git
```

2. Change to the directory for lab Terraform code:
```
cd content-deploying-to-aws-ansible-terraform/lab_jenkins_master_worker
```

3. Examine the contents of the directory you're in:
```
ls
```

### Run the gen_ssh_key.yaml Ansible Playbook to Generate SSH Key Pair

1. Run the Ansible Playbook:
```
ansible-playbook ansible_templates/gen_ssh_key.yaml
```
This Ansible Playbook will generate an SSH key pair for you user cloud_user which is required for deploying EC2 key pairs in our code.

Note: Alternatively, you may also run the following Linux command to do the same:
```
ssh-keygen -t rsa
```
When this command prompts for input, keep pressing enter until you're returned to the prompt. Do not enter a passphrase.

### Deploy the Terraform Code
1. Initialize the Terraform directory you changed into to download the required provider
```
terraform init
```
2. Ensure Terraform code is formatted properly:
```
terraform fmt
```
3. Ensure code has proper syntax and no errors:
```
terraform validat
```
4. See the execution plan and note the number of resources that will be created:
```
terraform plan
```
5. Deploy resources:
```
terraform apply
```

Enter yes when prompted.

After terraform apply has run successfully, you can either use the AWS CLI on the Controller node to list and describe created resources or you can log in to the AWS Console to verify and investigate created resources.

6. After a successful terraform apply, you will get the DNS URL of the ALB. Test it out to see if you can reach your Jenkins deployment.

Jenkins credentials:

username: admin
password: password
7. Finally, on the Terraform Controller node CLI, delete all resources which were created and ensure that it runs through successfully.
```
terraform destroy
```
Conclusion
Congratulations — you've completed this hands-on lab!