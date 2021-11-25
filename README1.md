# Setting up Cloud9 development environment.
STEP-1 : Create cloud9 environment

STEP-2 : Remove Temporary credentials 

rm -vf ${HOME}/.aws/credentials

STEP-3 : Create IAM role and assigned it to cloud9 environment.

STEP-4: Use the GetCallerIdentity CLI command line to check that Cloud9 IDE is using the correct IAM Role

aws sts get-caller-identity 

# Installing kubectl ( https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html )

sudo curl -o /usr/local/bin/kubectl  \
   https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl

sudo chmod +x /usr/local/bin/kubectl

kubectl version --client=true --short=true

# Install jq

sudo yum install -y jq

# Install bash-completion

sudo yum install -y bash-completion

# Install eksctl

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv -v /tmp/eksctl /usr/local/bin

eksctl version

# AWS CLOUD9 ADDITIONAL SETTINGS

1. Set default value to AWS Region that is currently using.

   export AWS_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')

   echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
   
   aws configure set default.region ${AWS_REGION}

   aws configure get default.region

2. Register the account ID you are currently working on as an environment variable.

   export ACCOUNT_ID=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.accountId')

   echo "export ACCOUNT_ID=${ACCOUNT_ID}" | tee -a ~/.bash_profile

3. Tutorial link : https://aws-eks-web-application.workshop.aws/en/50-eks-cluster/100-launch-cluster.html





