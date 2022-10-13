# Deployment of FortiGate-VM HA on the Oracle Cloud Infrastructure (OCI)
## Introduction
A Terraform script to deploy a FortiGate-VM HA Cluster Cross-AD on OCI

## Requirements
* [Terraform](https://learn.hashicorp.com/terraform/getting-started/install.html) >= 1.0.9
* Terraform Provider OCI >= 4.50
* Terraform Provider Template >= 2.2.0
* A [OCI API key](https://docs.cloud.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm)

## Deployment overview
Terraform deploys the following components:
   - A Virtual Cloud Network (VPC) with two public subnets
   - A VCN with two private subnets
   - Two FortiGate-VM instances with four NICs each in one AD.
   - Four firewall rules: one for external, one for internal, one for sync, and one for HA management.

## Deployment
To deploy the FortiGate-VMs to OCI:
1. Clone the repository.
2. Move the OCI API key and FortiGate-VM license file to the same folder
3. Customize variables in the `terraform.tfvars.example` and `variables.tf` file as needed.  And rename `terraform.tfvars.example` to `terraform.tfvars`.
4. Initialize the providers and modules:
   ```sh
   $ cd XXXXX
   $ terraform init
    ```
5. Submit the Terraform plan:
   ```sh
   $ terraform plan
   ```
6. Verify output.
7. Confirm and apply the plan:
   ```sh
   $ terraform apply
   ```
8. If output is satisfactory, type `yes`.

Output will include the information necessary to log in to the FortiGate-VM instances:
```sh
ClusterPublicIP = <FGT Public IP>
Default_Password = [
  "<FGT Password>",
]
Default_Username = admin
FGTActiveMGMTPublicIP = [
  "<FGT Active Public IP>",
]
FGTPassiveMGMTPublicIP = [
  "<FGT Passive Public IP>",
]
```
*After deployment, FortiGate-VM instances may not get the proper configurations during the initial bootstrap configuration. 
User may need to do a manual factoryreset on the units in order to get proper configurations.  To do a factoryreset, user can
login to the units via Console, and do `exec factoryreset`*

## Destroy the instance
To destroy the instance, use the command:
```sh
$ terraform destroy
```

# Support
Fortinet-provided scripts in this and other GitHub projects do not fall under the regular Fortinet technical support scope and are not supported by FortiCare Support Services.
For direct issues, please refer to the [Issues](https://github.com/fortinet/fortigate-terraform-deploy/issues) tab of this GitHub project.
For other questions related to this project, contact [github@fortinet.com](mailto:github@fortinet.com).

## License
[License](https://github.com/fortinet/fortigate-terraform-deploy/blob/master/LICENSE) © Fortinet Technologies. All rights reserved.

## Application Catalog/Image ID for deployment
Marketplace Catalog for mp_listing_id in variables.tf
BYOL 7.2.1: ocid1.image.oc1..aaaaaaaajnr54tko6kxnxc3q2u6rwfeu2rdfbyitbxecsqfih75j4jrdpxhq

Marketplace Image for mp_listing_resource_id in variables.tf
PAGY 7.2.1 2ocpu: ocid1.image.oc1..aaaaaaaajo5vcbgfaea6m244qfx7eptxhcxjlr2ypnzycqxjhwdviipk3ula
PAYG 7.2.1 4ocup: ocid1.image.oc1..aaaaaaaapxf2xbu55v5wus2fopkpjkh2zlunyzao6nnvuqni6l7va44acnza
PAYG 7.2.1 8ocup: ocid1.image.oc1..aaaaaaaaxqtgkltyonzin6emksvbodejf5f7wc3ddyy6zkfyl2jof5mwl6ta
PAYG 7.2.1 24ocup: ocid1.image.oc1..aaaaaaaamsj62krq74djb3b43p6jcluhpva5owvo2inotmbyba25zwwrhkva