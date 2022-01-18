# Домашнее задание к занятию "7.2. Облачные провайдеры и синтаксис Terraform."

---

## Задача 1  
  ~/DevOpsStudy/virt-homeworks/07-terraform-02-syntax/terraform   master *1 ❯ aws configure list  
      Name                    Value             Type    Location  
      ----                    -----             ----    --------  
   profile                <not set>             None    None  
access_key     ****************TOOC              env      
secret_key     ****************Luuq              env      
    region                us-west-2              env    AWS_DEFAULT_REGION  

## Задача 2  

можно использовать CloudFormation  
https://github.com/k-solomatin/virt-homeworks/tree/master/07-terraform-02-syntax/terraform  

### Листинг  

  ~/DevOpsStudy/virt-homeworks/07-terraform-02-syntax/terraform   master *1 ❯ terraform init  
Initializing the backend...  

Initializing provider plugins...  
- Reusing previous version of hashicorp/aws from the dependency lock file  
- Using previously-installed hashicorp/aws v3.31.0  

Terraform has been successfully initialized!  

You may now begin working with Terraform. Try running "terraform plan" to see  
any changes that are required for your infrastructure. All Terraform commands  
should now work.  

If you ever set or change modules or backend configuration for Terraform,  
rerun this command to reinitialize your working directory. If you forget, other  
commands will detect it and remind you to do so if necessary.  


  ~/DevOpsStudy/virt-homeworks/07-terraform-02-syntax/terraform   master *1 ❯ terraform plan  

An execution plan has been generated and is shown below.  
Resource actions are indicated with the following symbols:  
  \+ create  

Terraform will perform the following actions:  

  # aws_instance.web will be created  
  \+ resource "aws_instance" "web"  
   {
      \+ ami                          = "ami-0ca5c3bd5a268e7db"  
      \+ arn                          = (known after apply)  
      \+ associate_public_ip_address  = (known after apply)  
      \+ availability_zone            = (known after apply)  
      \+ cpu_core_count               = (known after apply)  
      \+ cpu_threads_per_core         = (known after apply)  
      \+ get_password_data            = false  
      \+ host_id                      = (known after apply)  
      \+ id                           = (known after apply)  
      \+ instance_state               = (known after apply)  
      \+ instance_type                = "t3.micro"  
      \+ ipv6_address_count           = (known after apply)  
      \+ ipv6_addresses               = (known after apply)  
      \+ key_name                     = (known after apply)  
      \+ outpost_arn                  = (known after apply)  
      \+ password_data                = (known after apply)  
      \+ placement_group              = (known after apply)  
      \+ primary_network_interface_id = (known after apply)  
      \+ private_dns                  = (known after apply)  
      \+ private_ip                   = (known after apply)  
      \+ public_dns                   = (known after apply)  
      \+ public_ip                    = (known after apply)  
      \+ secondary_private_ips        = (known after apply)  
      \+ security_groups              = (known after apply)  
      \+ source_dest_check            = true  
      \+ subnet_id                    = (known after apply)  
      \+ tags                         = {  
          \+ "Name" = "HelloWorld"  
        }  
      \+ tenancy                      = (known after apply)  
      \+ vpc_security_group_ids       = (known after apply)  

      \+ ebs_block_device {  
          \+ delete_on_termination = (known after apply)  
          \+ device_name           = (known after apply)  
          \+ encrypted             = (known after apply)  
          \+ iops                  = (known after apply)  
          \+ kms_key_id            = (known after apply)  
          \+ snapshot_id           = (known after apply)  
          \+ tags                  = (known after apply)  
          \+ throughput            = (known after apply)  
          \+ volume_id             = (known after apply)  
          \+ volume_size           = (known after apply)  
          \+ volume_type           = (known after apply)  
        }  

      \+ enclave_options {  
          \+ enabled = (known after apply)  
        }  

      \+ ephemeral_block_device {  
          \+ device_name  = (known after apply)  
          \+ no_device    = (known after apply)  
          \+ virtual_name = (known after apply)  
        }  

      \+ metadata_options {  
          \+ http_endpoint               = (known after apply)  
          \+ http_put_response_hop_limit = (known after apply)  
          \+ http_tokens                 = (known after apply)  
        }  

      \+ network_interface {  
          \+ delete_on_termination = (known after apply)  
          \+ device_index          = (known after apply)  
          \+ network_interface_id  = (known after apply)  
        }  

      \+ root_block_device {  
          \+ delete_on_termination = (known after apply)  
          \+ device_name           = (known after apply)  
          \+ encrypted             = (known after apply)  
          \+ iops                  = (known after apply)  
          \+ kms_key_id            = (known after apply)  
          \+ tags                  = (known after apply)  
          \+ throughput            = (known after apply)  
          \+ volume_id             = (known after apply)  
          \+ volume_size           = (known after apply)  
          \+ volume_type           = (known after apply)  
        }  
    }  

Plan: 1 to add, 0 to change, 0 to destroy.  

------------------------------------------------------------------------  

Note: You didn't specify an "-out" parameter to save this plan, so Terraform  
can't guarantee that exactly these actions will be performed if  
"terraform apply" is subsequently run.  






  ~/DevOpsStudy/virt-homeworks/07-terraform-02-syntax/terraform   master *1 ❯ terraform apply  

An execution plan has been generated and is shown below.  
Resource actions are indicated with the following symbols:  
  \+ create  

Terraform will perform the following actions:  

  # aws_instance.web will be created  
  \+ resource "aws_instance" "web" {  
      \+ ami                          = "ami-0ca5c3bd5a268e7db"  
      \+ arn                          = (known after apply)  
      \+ associate_public_ip_address  = (known after apply)  
      \+ availability_zone            = (known after apply)  
      \+ cpu_core_count               = (known after apply)  
      \+ cpu_threads_per_core         = (known after apply)  
      \+ get_password_data            = false  
      \+ host_id                      = (known after apply)  
      \+ id                           = (known after apply)  
      \+ instance_state               = (known after apply)  
      \+ instance_type                = "t3.micro"  
      \+ ipv6_address_count           = (known after apply)  
      \+ ipv6_addresses               = (known after apply)  
      \+ key_name                     = (known after apply)  
      \+ outpost_arn                  = (known after apply)  
      \+ password_data                = (known after apply)  
      \+ placement_group              = (known after apply)  
      \+ primary_network_interface_id = (known after apply)  
      \+ private_dns                  = (known after apply)  
      \+ private_ip                   = (known after apply)  
      \+ public_dns                   = (known after apply)  
      \+ public_ip                    = (known after apply)  
      \+ secondary_private_ips        = (known after apply)  
      \+ security_groups              = (known after apply)  
      \+ source_dest_check            = true  
      \+ subnet_id                    = (known after apply)  
      \+ tags                         = {  
          \+ "Name" = "HelloWorld"  
        }  
      \+ tenancy                      = (known after apply)  
      \+ vpc_security_group_ids       = (known after apply)  

      \+ ebs_block_device {  
          \+ delete_on_termination = (known after apply)  
          \+ device_name           = (known after apply)  
          \+ encrypted             = (known after apply)  
          \+ iops                  = (known after apply)  
          \+ kms_key_id            = (known after apply)  
          \+ snapshot_id           = (known after apply)  
          \+ tags                  = (known after apply)  
          \+ throughput            = (known after apply)  
          \+ volume_id             = (known after apply)  
          \+ volume_size           = (known after apply)  
          \+ volume_type           = (known after apply)  
        }  

      \+ enclave_options {  
          \+ enabled = (known after apply)  
        }  

      \+ ephemeral_block_device {  
          \+ device_name  = (known after apply)  
          \+ no_device    = (known after apply)  
          \+ virtual_name = (known after apply)  
        }  

      \+ metadata_options {  
          \+ http_endpoint               = (known after apply)  
          \+ http_put_response_hop_limit = (known after apply)  
          \+ http_tokens                 = (known after apply)  
        }  

      \+ network_interface {  
          \+ delete_on_termination = (known after apply)  
          \+ device_index          = (known after apply)  
          \+ network_interface_id  = (known after apply)  
        }  

      \+ root_block_device {  
          \+ delete_on_termination = (known after apply)  
          \+ device_name           = (known after apply)  
          \+ encrypted             = (known after apply)  
          \+ iops                  = (known after apply)  
          \+ kms_key_id            = (known after apply)  
          \+ tags                  = (known after apply)  
          \+ throughput            = (known after apply)  
          \+ volume_id             = (known after apply)  
          \+ volume_size           = (known after apply)  
          \+ volume_type           = (known after apply)  
        }  
    }  

Plan: 1 to add, 0 to change, 0 to destroy.  

Do you want to perform these actions?  
  Terraform will perform the actions described above.  
  Only 'yes' will be accepted to approve.  

  Enter a value: yes  

aws_instance.web: Creating...  
aws_instance.web: Still creating... [10s elapsed]  
aws_instance.web: Still creating... [20s elapsed]  
aws_instance.web: Creation complete after 28s [id=i-0b0a9da8b816e7f1c]  

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.  


---
