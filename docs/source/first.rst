First Steps
=================

.. _first:

Create Your AWS Account
-----------------------

Follow these steps to create a new billing account : https://portal.aws.amazon.com/billing/signup#/start

Active IAM Billing Access from the Account page : https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/control-access-billing.html#ControllingAccessWebsite-Activate

Active SSO in the region of your choice, This will also create the AWS Organization



Terraform or CloudFormation
----------------------------

You will now have to choose which Infrastructure as Code service.  Both are very different implemnentations

the Bedrock Foundation is available in both CloudFormation (cfn folder) and Terraform (tf folder) in the repository. 

If you are unsure, create two seperate management accounts, and try both. 


Feature Set Comparison Tables
------------------------------

Insert Table


Git Repository Authentication
-----------------------------

The Bedrock Foundation uses OIDC to authenticate with GitHub, Bitbucket and Gitlab. There is no requirement to have IAM keys
