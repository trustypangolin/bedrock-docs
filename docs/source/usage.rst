Usage
=====
.. autosummary::
    :toctree: generated
.. _usage:

Quick Start Landing Zone Code
-----------------------------------
To use Bedrock Landing Zone, first fork/clone the Repo with your preferred CI/CD framework:

**GitHub Actions**

.. code-block:: console

    git clone https://github.com/trustypangolin/bedrock-foundation-template

**BitBucket Pipelines**

.. code-block:: console

    git clone https://bitbucket.org/trustypangolin/bedrock-foundation-template

**GitLab Pipelines**

.. code-block:: console

    git clone https://gitlab.com/trustypangolin/bedrock-foundation-template


Management AWS Account
-----------------------------------
The landing zone will need the initial AWS account to be created. All other sub accounts are created as part of the CI/CD process


Add The Variables in your Git Secrets
-------------------------------------

.. list-table:: Git Secrets/Variables to set
   :widths: 25 25 50
   :header-rows: 1

   * - Repository Secrets, Variables
     - Example
     - Description
   * - ``AWS_ROOT_ACCOUNT``
     - ``111111111111``
     - | Your 12 digit AWS Management Account ID
   * - ``BEDROCK_TF_STATE`` (Optional)
     - ``dGVycmFmb3JtIHsKICBiYWNrZW5kICJzMyIge``
       ``wogICAgcmVnaW9uICAgICAgICAgPSAiYXAtc2``
       ``91dGhlYXN0LTIiCiAgICBkeW5hbW9kYl90YWJ``
       ``sZSA9ICJiZWRyb2NrLXRmc3RhdGUiCiAgfQp9``
     - | Single line Base64 version of the ``remote_state.tf``
       | Note that Key and Bucket are not included. 
   * - ``BEDROCK_TF_VARS`` (Optional)
     - ``dW5pcXVlX3ByZWZpeCA9ICJpbmRpZ29jYXB5Ym``
       ``FyYSIgIApiYXNlX3JlZ2lvbiA9ICJhcC1zb3V0``
       ``aGVhc3QtMiIKcm9vdF9lbWFpbHMgPSB7CiAgIl``
       ``NlY3VyaXR5IiAgID0gImF3cytiZWRyb2NrLnNl``
       ``Y0Bkb21haW4iCiAgIlNoYXJlZCIgICAgID0gIm``
       ``F3cytiZWRyb2NrLnNoYXJlZEBkb21haW4iCiAg``
       ``IlByb2R1Y3Rpb24iID0gImF3cytiZWRyb2NrLn``
       ``Byb2RAZG9tYWluIgp9Cm5vdGlmaWNhdGlvbnMg``
       ``PSB7CiAgYmlsbGluZyAgICA9ICJhd3MrYmVkcm``
       ``9jay5iaWxsaW5nQGRvbWFpbiIKICBvcGVyYXRp``
       ``b25zID0gImF3cytiZWRyb2NrLm9wZXJhdGlvbn``
       ``NAZG9tYWluIgogIHNlY3VyaXR5ICAgPSAiYXdz``
       ``K2JlZHJvY2suc2VjdXJpdHlAZG9tYWluIgp9``
     - | Single line Base64 version of the ``terraform.tfvars``
   * - ``ENCKEY``
     - Password123!
     - | Artifacts such as STS credentials are encoded between 
       | jobs with OpenSSL, so that non-admins can't access temporary 
       | credentials from an artifcats file
  

Bootstrap your AWS Managment Account
------------------------------------

You will need the AWS CLI tools and a local copy of Terraform installed
  
#. Activate SSO in your preferred region
#. Configure SSO with the preferred IdP (eg AWS/Azure/Google/OKTA). 
#. Create and Assign yourself AdministratorAccess permissions via the PermissionsSets to the Management Account
#. Log into the AWS account landing page (http://d-someid.awsapps.com/start)
#. Either grab the temporary keys from the AWS Landing Page and input them into the ``~/.aws/credentials`` file, or 
#. configure your ``~/.aws/config`` file for SSO and use ``aws sso login --profile <your profile>``
#. Ensure the credentials/profile is set as default by setting ``export AWS_PROFILE=<your profile>``

You should now have admin access to the account via SSO, confirmed by running a simple cli command such as ``aws organizations list-roots`` should return organizations values for the Management account Id 

You now need a way for GitHub/GitLab/BitBucket to have access to your new AWS account, there is some terraform files in the /tf folder that will allow you bootstrap the various OIDC and roles required

#. copy the terraform.tfvars.template file to terraform.tfvars and 
#. change the values to suit your repo and naming for the OIDC
#. terraform init
#. terraform apply

Your CI/CD process should now be able to assume the basic roles setup if you set the repo values up corectly