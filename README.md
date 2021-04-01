# Terraform 
- Infrastructure as code tool
- Access among multiple providers such as AWS, GCP, Azure,etc

## Terraform Providers 
- plugin to talk to a specific set of APIs
- providers that terraform supports eg . AWS
- So we need to set up the configuration for the provider we need

## Terraform Basic Commands
`terraform init` 
- going to look into all the configuration in the main.tf file
- will download all the plugins for all the providers, eg. AWS, Azure, GCP
- adds a .terraform/init folder with all the plugins

`terraform plan`
- does a dry run of the code
- will show if it will delete any instances modify instances
- quick sanity check to check for any changes

`terraform apply`
- runs another dry run
- executes the commands to run application
- will always refresh terraform.tfstate
- running apply again doesn't deploy the resource again
- terraform apply --auto-approve
	- skips having to type on YES all the time

`terraform destroy`
- destroys the resources defined in terraform

Other Notes
- Order of the resources of code does not matter in terraform
- No matter how many times we apply terraform, we give it the blueprint, 
- We define what our entire infrastructure looks like, state will always match what is in terraform code
- The state is always refreshed when you click on apply, it will figure out what needs to be added changed or destroyed

File: `terraform.tfstate`
- will always contains what is deployed in the provider, eg. aws
- DO NOT mess with this file. it will destroy terraform and will create mismatches in your configuration


`main.tf`
- contains definition for resources 

`output.tf` 
- will print the values of the resources we want to deploy 

`provider.tf`
- providers for the APIs we're using eg. aws, gcp or azure

`state_config.tf`
- can configure it to check state via storage eg. s3 , this useful for teams where people are modifying and deploying new resources

`terraform.tfvars` 
- never pushed keep all your vars here, will be read in variables.tf

`variables.tf `
- where we define the variables we're going to use
- this is where they're declared


## Terraform Troubleshooting and Debugging
- Setting console logging to verbose
- Useful for debugging deployment issues

Set logging to verbose
```bash
$ export TF_LOG=true
```

Unset logging
```bash
$ export TF_LOG=
```

## Common Errors

### State is locked
```bash
Error locking state: Error acquiring the state lock: ConditionalCheckFailedException: The conditional request failed
ID:        xxxxxxxx-1386-5164-fe11-bbb268404105
Path:      xxxxxxxxx-ap-southeast-1-terraform-state/aws-ecr-terraform.tfstate
Operation: OperationTypeApply
Who:       eddrichjanzzenang@eja.lan
Version:   0.14.8
Created:   2021-03-29 13:42:43.630445 +0000 UTC
Info:

```

### Solution:
```bash
# terraform force-unlock <ID>
$ terraform force-unlock xxxxxxxx-1386-5164-fe11-bbb268404105
```


