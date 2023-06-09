# Steps to setup AFT

### Prep Terraform Environment for AFT deployment:

1. Create and enroll AFT-Management account.

2. Create Cloud9 IDE using following commands:
```
   > git clone --branch aft-cloud9 https://github.com/aws-samples/aft-workshop-sample.git aft-cloud9
   > cd aft-cloud9
   > ./cloud9.sh {{CT-HOME-REGION}} false
```
This script installs terraform along with creating Cloud9 IDE.

3. From your Cloud9 console, select the Cloud9 > Preferences.
   From the Preferences window, choose AWS Settings > Credentials
   Disable the AWS managed temporary credentials
-----

### AFT Deployment:

1. Clone the [example repository](https://github.com/hashicorp/learn-terraform-aws-control-tower-aft) containing the AFT module configuration.

   `git clone https://github.com/hashicorp/learn-terraform-aws-control-tower-aft `
   
2. Fork the four account configuration repositories into your personal Github account.

    The [learn-terraform-aft-account-request](https://github.com/hashicorp/learn-terraform-aft-account-request) repository, which contains example configuration to kick off new account provisioning using AFT.
    The [learn-terraform-aft-global-customizations](https://github.com/hashicorp/learn-terraform-aft-global-customizations) repository, which contains boilerplate configuration for customizations to apply to all accounts created by AFT.
    The [learn-terraform-aft-account-customizations](https://github.com/hashicorp/learn-terraform-aft-account-customizations) repository, which contains boilerplate configuration for account-specific customizations.
    The [learn-terraform-aft-account-provisioning-customizations](https://github.com/hashicorp/learn-terraform-aft-account-provisioning-customizations) repository, which contains boilerplate configuration for provisioning-time customizations to apply to accounts.

3. Clone your copies of the repositories.  
   ```
   > git clone https://github.com/USERNAME/learn-terraform-aft-account-request
   > git clone https://github.com/USERNAME/learn-terraform-aft-global-customizations
   > git clone https://github.com/USERNAME/learn-terraform-aft-account-customizations
   > git clone https://github.com/USERNAME/learn-terraform-aft-account-provisioning-customizations
   ```
4. Deploy AFT module - Update main.tf file in `learn-terraform-aws-control-tower-aft` and run `terraform init -update` followed by `terraform apply`.
5. Enable Codestar connection in AFT Management account.
6. Add AFTExecutionRole to Control Tower portfolio.
7. Enroll your first Sandbox account by configuring tf files in `learn-terraform-aft-account-request`.
 
