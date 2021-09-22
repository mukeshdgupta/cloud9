# TOOLS AND RESOURCES
Install text utilities
sudo yum -y install jq gettext
# 2. Set up env-vars.sh script
This script defines a function that records a trail of all environment variables that are needed in the course of the workshop. This makes it easy to re-use environment variables across multiple terminal sessions in Cloud9.

cat <<EoF > ~/env-vars.sh
#!/bin/bash

save_var() {
  if [ \$? -eq 0 ]; then
    export \$1=\$2
    echo export \$1=\$2 >> ~/env-vars.sh
  fi
}
EoF
chmod +x ~/env-vars.sh
source ~/env-vars.sh
echo "[[ -s ~/env-vars.sh ]] && source ~/env-vars.sh" >> ~/.bash_profile
  
# 3. Configure the AWS CLI with our current region as default:
  
save_var AWS_REGION $(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r .region)
aws configure set default.region ${AWS_REGION}
aws configure get default.region

# 4. Set up env variable for account id
  
save_var AWS_ACCOUNT_ID $(aws sts get-caller-identity --query Account --output text)
 
# 5 Enable Cloudwatch Container Insights
Enable Cloudwatch Container Insights as follows:

aws ecs put-account-setting-default --name containerInsights --value enabled
To verify that Container Insights has been enabled, use:

aws ecs list-account-settings --effective-settings --name containerInsights
  
