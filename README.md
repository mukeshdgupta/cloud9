# cloud9
cloud9 environment setup for the development.

Steps to increase size of cloud9 instance:

Step-1 : touch resize.sh && chmod +x resize.sh

Step-2 : ./resize.sh 20

Step-3: lsblk 

Step-4: aws configure get default.region

# To bootstrap the environment 
Step-6: cdk bootstrap aws://117134819170/us-west-1
