# Домашнее задание к занятию "7.2. Облачные провайдеры и синтаксис Terraform."

Зачастую разбираться в новых инструментах гораздо интересней понимая то, как они работают изнутри.
Поэтому в рамках первого *необязательного* задания предлагается завести свою учетную запись в AWS (Amazon Web Services) или Yandex.Cloud.
Идеально будет познакомится с обоими облаками, потому что они отличаются.

## Задача 1 (вариант с AWS). Регистрация в aws и знакомство с основами (необязательно, но крайне желательно).

Остальные задания можно будет выполнять и без этого аккаунта, но с ним можно будет увидеть полный цикл процессов.

AWS предоставляет достаточно много бесплатных ресурсов в первых год после регистрации, подробно описано [здесь](https://aws.amazon.com/free/).
1. Создайте аккаут aws.
1. Установите c aws-cli https://aws.amazon.com/cli/.
1. Выполните первичную настройку aws-sli https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html.
1. Создайте IAM политику для терраформа c правами
    * AmazonEC2FullAccess
    * AmazonS3FullAccess
    * AmazonDynamoDBFullAccess
    * AmazonRDSFullAccess
    * CloudWatchFullAccess
    * IAMFullAccess
1. Добавьте переменные окружения
    ```
    export AWS_ACCESS_KEY_ID=(your access key id)
    export AWS_SECRET_ACCESS_KEY=(your secret access key)
    ```
1. Создайте, остановите и удалите ec2 инстанс (любой с пометкой `free tier`) через веб интерфейс.

В виде результата задания приложите вывод команды `aws configure list`.

## Задача 1 (Вариант с Yandex.Cloud). Регистрация в aws и знакомство с основами (необязательно, но крайне желательно).

1. Подробная инструкция на русском языке содержится [здесь](https://cloud.yandex.ru/docs/solutions/infrastructure-management/terraform-quickstart).
2. Обратите внимание на период бесплатного использования после регистрации аккаунта.
3. Используйте раздел "Подготовьте облако к работе" для регистрации аккаунта. Далее раздел "Настройте провайдер" для подготовки
базового терраформ конфига.
4. Воспользуйтесь [инструкцией](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs) на сайте терраформа, что бы
не указывать авторизационный токен в коде, а терраформ провайдер брал его из переменных окружений.

## Задача 2. Созданием aws ec2 или yandex_compute_instance через терраформ.

1. В каталоге `terraform` вашего основного репозитория, который был создан в начале курсе, создайте файл `main.tf` и `versions.tf`.
2. Зарегистрируйте провайдер
   1. для [aws](https://registry.terraform.io/providers/hashicorp/aws/latest/docs). В файл `main.tf` добавьте
   блок `provider`, а в `versions.tf` блок `terraform` с вложенным блоком `required_providers`. Укажите любой выбранный вами регион
   внутри блока `provider`.
   2. либо для [yandex.cloud](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs). Подробную инструкцию можно найти
   [здесь](https://cloud.yandex.ru/docs/solutions/infrastructure-management/terraform-quickstart).
3. Внимание! В гит репозиторий нельзя пушить ваши личные ключи доступа к аккаунту. Поэтому в предыдущем задании мы указывали
их в виде переменных окружения.
4. В файле `main.tf` воспользуйтесь блоком `data "aws_ami` для поиска ami образа последнего Ubuntu.  
5. В файле `main.tf` создайте рессурс
   1. либо [ec2 instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance).
   Постарайтесь указать как можно больше параметров для его определения. Минимальный набор параметров указан в первом блоке
   `Example Usage`, но желательно, указать большее количество параметров.
   2. либо [yandex_compute_image](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/compute_image).
6. Также в случае использования aws:
   1. Добавьте data-блоки `aws_caller_identity` и `aws_region`.
   2. В файл `outputs.tf` поместить блоки `output` с данными об используемых в данный момент:
       * AWS account ID,
       * AWS user ID,
       * AWS регион, который используется в данный момент,
       * Приватный IP ec2 инстансы,
       * Идентификатор подсети в которой создан инстанс.  
7. Если вы выполнили первый пункт, то добейтесь того, что бы команда `terraform plan` выполнялась без ошибок.


В качестве результата задания предоставьте:
1. Ответ на вопрос: при помощи какого инструмента (из разобранных на прошлом занятии) можно создать свой образ ami?
1. Ссылку на репозиторий с исходной конфигурацией терраформа.  

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
  + create  

Terraform will perform the following actions:  

  # aws_instance.web will be created  
  + resource "aws_instance" "web" {  
      + ami                          = "ami-0ca5c3bd5a268e7db"  
      + arn                          = (known after apply)  
      + associate_public_ip_address  = (known after apply)  
      + availability_zone            = (known after apply)  
      + cpu_core_count               = (known after apply)  
      + cpu_threads_per_core         = (known after apply)  
      + get_password_data            = false  
      + host_id                      = (known after apply)  
      + id                           = (known after apply)  
      + instance_state               = (known after apply)  
      + instance_type                = "t3.micro"  
      + ipv6_address_count           = (known after apply)  
      + ipv6_addresses               = (known after apply)  
      + key_name                     = (known after apply)  
      + outpost_arn                  = (known after apply)  
      + password_data                = (known after apply)  
      + placement_group              = (known after apply)  
      + primary_network_interface_id = (known after apply)  
      + private_dns                  = (known after apply)  
      + private_ip                   = (known after apply)  
      + public_dns                   = (known after apply)  
      + public_ip                    = (known after apply)  
      + secondary_private_ips        = (known after apply)  
      + security_groups              = (known after apply)  
      + source_dest_check            = true  
      + subnet_id                    = (known after apply)  
      + tags                         = {  
          + "Name" = "HelloWorld"  
        }  
      + tenancy                      = (known after apply)  
      + vpc_security_group_ids       = (known after apply)  

      + ebs_block_device {  
          + delete_on_termination = (known after apply)  
          + device_name           = (known after apply)  
          + encrypted             = (known after apply)  
          + iops                  = (known after apply)  
          + kms_key_id            = (known after apply)  
          + snapshot_id           = (known after apply)  
          + tags                  = (known after apply)  
          + throughput            = (known after apply)  
          + volume_id             = (known after apply)  
          + volume_size           = (known after apply)  
          + volume_type           = (known after apply)  
        }  

      + enclave_options {  
          + enabled = (known after apply)  
        }  

      + ephemeral_block_device {  
          + device_name  = (known after apply)  
          + no_device    = (known after apply)  
          + virtual_name = (known after apply)  
        }  

      + metadata_options {  
          + http_endpoint               = (known after apply)  
          + http_put_response_hop_limit = (known after apply)  
          + http_tokens                 = (known after apply)  
        }  

      + network_interface {  
          + delete_on_termination = (known after apply)  
          + device_index          = (known after apply)  
          + network_interface_id  = (known after apply)  
        }  

      + root_block_device {  
          + delete_on_termination = (known after apply)  
          + device_name           = (known after apply)  
          + encrypted             = (known after apply)  
          + iops                  = (known after apply)  
          + kms_key_id            = (known after apply)  
          + tags                  = (known after apply)  
          + throughput            = (known after apply)  
          + volume_id             = (known after apply)  
          + volume_size           = (known after apply)  
          + volume_type           = (known after apply)  
        }  
    }  

Plan: 1 to add, 0 to change, 0 to destroy.  

------------------------------------------------------------------------  

Note: You didn't specify an "-out" parameter to save this plan, so Terraform  
can't guarantee that exactly these actions will be performed if  
"terraform apply" is subsequently run.  
  

---
