# Steps to setup AFT

### Prep Terraform Environment for AFT deployment:

1. Create and enroll AFT-Management account.

2. Create Cloud9 IDE using following commands:
```
   git clone --branch aft-cloud9 https://github.com/aws-samples/aft-workshop-sample.git aft-cloud9
```
```
   cd aft-cloud9
```
```
   ./cloud9.sh {{CT-HOME-REGION}} false
```
This script installs terraform along with creating Cloud9 IDE.

3. From your Cloud9 console, select the Cloud9 > Preferences.
   From the Preferences window, choose AWS Settings > Credentials
   Disable the AWS managed temporary credentials
-----

### AFT Deployment:

1. Clone the [example repository](https://github.com/hashicorp/learn-terraform-aws-control-tower-aft) containing the AFT module configuration.

   ```
   git clone https://github.com/hashicorp/learn-terraform-aws-control-tower-aft 
   ```
   
2. Fork the four account configuration repositories into your personal Github account.

    The [learn-terraform-aft-account-request](https://github.com/hashicorp/learn-terraform-aft-account-request) repository, which contains example configuration to kick off new account provisioning using AFT.
    
    The [learn-terraform-aft-global-customizations](https://github.com/hashicorp/learn-terraform-aft-global-customizations) repository, which contains boilerplate configuration for customizations to apply to all accounts created by AFT.
    
    The [learn-terraform-aft-account-customizations](https://github.com/hashicorp/learn-terraform-aft-account-customizations) repository, which contains boilerplate configuration for account-specific customizations.
    
    The [learn-terraform-aft-account-provisioning-customizations](https://github.com/hashicorp/learn-terraform-aft-account-provisioning-customizations) repository, which contains boilerplate configuration for provisioning-time customizations to apply to accounts.

3. Clone your copies of the repositories.  
   ```
   git clone https://github.com/USERNAME/learn-terraform-aft-account-request
   ```
   ```
   git clone https://github.com/USERNAME/learn-terraform-aft-global-customizations
   ```
   ```
   git clone https://github.com/USERNAME/learn-terraform-aft-account-customizations
   ```
   ```
   git clone https://github.com/USERNAME/learn-terraform-aft-account-provisioning-customizations
   ```
4. Deploy AFT module - Update main.tf file in `learn-terraform-aws-control-tower-aft` and run `terraform init -upgrade` followed by `terraform apply`.
5. Enable Codestar connection in AFT Management account.
6. Add AFTExecutionRole to Control Tower portfolio.
7. Enroll your first Sandbox account by configuring tf files in `learn-terraform-aft-account-request`.

![image](https://github.com/saravram/AFT/assets/45466472/16951079-9f67-46c0-a5fd-cef984be20e8)58b5bf337d37)


8. Global customization sample module:

```
account = $(aws sts get-caller-identity --query Account --output text)
region = $(aws ec2 describe-availability-zones --query 'AvailabilityZones[0].[RegionName]' --output text)
cidr = $(python ./python/source/get_cidr_range.py)
aws ssm put-parameter --name /$account/$region/vpc/cidr --value $cidr
```

```
resource "aws_s3_account_public_access_block" "block_all_public" {
  block_public_acls   = true
  block_public_policy = true
  ignore_public_acls  = true
  restrict_public_buckets  = true
}
```

### Resources:
1. Installing terraform - https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
2. To configure different vcs provider - https://github.com/aws-ia/terraform-aws-control_tower_account_factory/tree/main/examples
3. Install AFT main.tf inputs - https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
4. Account request sample code - https://github.com/aws-ia/terraform-aws-control_tower_account_factory/tree/main/sources/aft-customizations-repos/aft-account-request
5. Re-invoke customization - https://docs.aws.amazon.com/controltower/latest/userguide/aft-account-customization-options.html#aft-re-invoke-customizations
