Terraform
=================

.. autosummary::
    :toctree: generated

OIDC Terraform files
----------------------

AWS will require the correct OIDC settings depending on your Git provider

The following OIDC tf files have been included, along with associated pipeline setups

1. Gitlab (CI/CD)          ``gitlab-oidc.tf`` and ``.gitlab-ci.yml`` CI/CD
2. Github (Github Actions) ``github-oidc.tf`` and ``.github`` folder with Github Actions
3. Bitbucket (Pipelines)   ``bitbucket-oidc.tf`` and ``bitbucket-pipelines.yml`` Pipelines

There is some initial bootstrapping involved with Terraform before the pipeline code can takeover the hardwork

Customising the Terraform environment variables
---------------------

First, open a cli and move into the tf folder

``cd /tf``

copy the ``terraform.tfvars.template`` to ``terraform.tfvars``

``cp terraform.tfvars.template terraform.tfvars``

this file should stay untracked in your repo via ``.gitignore``, as it will generally have secret or semi-secret information


Intialise Terraform
-------------------

Ensure terraform has been installed

rename the git repository tf files that are not utilised to -oidc.tf.disabled, however leaving them as-is will not give additonal access without proper variables