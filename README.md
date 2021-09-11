# cloud9
cloud9 environment setup for the development.

Steps to increase size of cloud9 instance:

Step-1 : touch resize.sh && chmod +x resize.sh

Step-2 : ./resize.sh 20

Step-3: lsblk 

Step-4: aws configure get default.region

# To bootstrap the environment 
Step-6: cdk bootstrap aws://117134819170/us-west-1

# Install kubectl

sudo curl --silent --location -o /usr/local/bin/kubectl \
   https://amazon-eks.s3.us-west-2.amazonaws.com/1.17.11/2020-09-18/bin/linux/amd64/kubectl

sudo chmod +x /usr/local/bin/kubectl

# Update awscli

sudo pip install --upgrade awscli && hash -r

# AWS CLI Installed
aws --version

# To check and install jq
sudo yum install -y jq
export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
export AWS_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')
echo "export ACCOUNT_ID=${ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region

link : https://cicd-pipeline-cdk-eks-bluegreen.workshop.aws/en/intro/prepare.html

# Download and install Kubectl and IAM Authenticator:

curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
kubectl help
curl -o aws-iam-authenticator https://amazon-eks.s3.us-west-2.amazonaws.com/1.15.10/2020-02-22/bin/linux/amd64/aws-iam-authenticator
chmod +x ./aws-iam-authenticator
mkdir -p $HOME/bin && cp ./aws-iam-authenticator $HOME/bin/aws-iam-authenticator && export PATH=$PATH:$HOME/bin
echo 'export PATH=$PATH:$HOME/bin' >> ~/.bashrc

# Install pre-requisite packages for the CDK

sudo yum install -y npm
npm install -g aws-cdk@1.30.0 --force
npm install -g typescript@latest

