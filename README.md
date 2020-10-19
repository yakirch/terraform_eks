# terraform_eks
#This repo contain basic setup for AWS EKS using Terraform.

Environment:

AWS env 
Terraform will be executed from a Linux EC2 instance

Prerequisites:

On the Linux unit install:
AWS account with IAM permissions as listed in https://github.com/terraform-aws-modules/terraform-aws-eks/blob/master/docs/iam-permissions.md
AWS CLI
AWS IAM Authenticator
jq
kubectl
Terraform 


IAM role attach:
Attach the IAM role to the EC2 instance using the aws ec2 console.
rm -vf ${HOME}/.aws/credentials
verify correct IAM role, run: aws sts get-caller-identity
export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
export AWS_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')
aws configure set default.region ${AWS_REGION}


Deploy:

Login to the Linux terraform unit.
clone this repository
cd to the repo folder
run 'terraform init'
run 'terraform apply'

It takes 10-20 minutes to start the EKS cluster.

to verify cluster is running run :

kubectl get nodes -o wide


