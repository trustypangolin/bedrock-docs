Operational
==========

.. autosummary::
    :toctree: generated

    Bedrock

Account Design
----------------------

.. image:: drawio/Bedrock-Operational.png
  :alt: Operational Account High Level Design


Operational Excellence Design
----------------------

.. image:: drawio/Bedrock-Operational-Operational.png
  :alt: Operational Excellence High Level Design

Cost Optimisation Design
----------------------

Scheduler has a role in these accounts, actual Lambda and CloudWatch schedule is in the Central account

.. image:: drawio/Bedrock-Operational-CostOp.png
  :alt: Cost Optimisation High Level Design

Reliability Design
----------------------

AWS Backup is set from the Organisation Level, refer to Management-Reliability

.. image:: drawio/Bedrock-Operational-Reliability.png
  :alt: Reliability High Level Design

Security Design
----------------------

.. image:: drawio/Bedrock-Operational-Security.png
  :alt: Security High Level Design
