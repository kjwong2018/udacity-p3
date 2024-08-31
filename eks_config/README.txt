# Create IAM Role
aws iam create-role --role-name myAmazonEKSClusterRole --assume-role-policy-document file://"eks-cluster-role-trust-policy.json"

# Attach pollicy to IAM Role
aws iam attach-role-policy --policy-arn arn:aws:iam::aws:policy/AmazonEKSClusterPolicy --role-name myAmazonEKSClusterRole

# Run the following to create your EKS cluster
aws eks create-cluster --region us-east-1 --name kjwong-udacity-udagram --kubernetes-version 1.30 \
   --role-arn [REDACTED] \
   --resources-vpc-config subnetIds=subnet-0886f7a4543ec636c,subnet-0edf10977df89837e

# Check status of cluster creation
aws eks describe-cluster --region us-east-1 --name kjwong-udacity-udagram --query "cluster.status"

# Update kubeconfig after node group creation
aws eks update-kubeconfig --region us-east-1 --name kjwong-udacity-udagram

# Deploy everything in secret-deployment and app-deployment (do no upload secret yaml file to gitlab)