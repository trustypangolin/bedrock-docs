Usage
=====
.. autosummary::
    :toctree: generated
.. _usage:

Clone the Landing Zone Code
-----------------------------------
To use Bedrock Landing Zone, first clone the Repo:

.. code-block:: console

    git clone https://github.com/trustypangolin/bedrock-foundation-template
    git clone https://bitbucket.org/trustypangolin/bedrock-foundation-template
    git clone https://gitlab.com/trustypangolin/bedrock-foundation-template


Creating the Management AWS Account
-----------------------------------
The landing zone will need the initial AWS account to be created. All other sub accounts are created as part of the IaC


Add The Variables in your Git Secrets
-------------------------------------

| AWS_ROOT_ACCOUNT: Your Management Account ID
| BEDROCK_TF_STATE: a Base64 encoded version of the remote_state.tf file. This is your S3 remote state file setup
| BEDROCK_TF_VARS: a Base64 encoded version of terraform.tfvars file. This is your main variables file
| ENCKEY: To keep artifcats encrypted, we set a complex password here that openssl uses to encode artifacts between jobs

Bootstrap your AWS Managment Account
------------------------------------

| Activate SSO in your preferred region
| Add your account via whatever OAuth you have used (eg AWS/Azure/Google/OKTA). 
| Assign yourself AdministratorAccess permissions via the PermissionsSets to the Management Account, 
| Log into the AWS account landing page (http://d-someid.awsapps.ocm/start)
| Either grab the keys from the landing page, or configure your CLI for SSO and use aws sso login --profile <whatever>

You should now have admin access to the account via SSO, confirm by running a simple cli command

You now need a way for GitHub/GitLab/BitBucket to have access to your new AWS account, there is some terraform files in the /tf folder that will allow you bootstrap the various OIDC and roles required

| copy the terraform.tfvars.template file to terraform.tfvars and change the values to suit your repo and naming
| intiialise and apply the terraform config to bootstrap the OIDC
| terraform init
| terraform apply

Your CI/CD process should now be able to assume the basic roles setup if you set the repo values up corectly