# Домашнее задание к занятию "7.6. Написание собственных провайдеров для Terraform."

1.  
    resource = https://github.com/hashicorp/terraform-provider-aws/blob/8e4d8a3f3f781b83f96217c2275f541c893fec5a/aws/provider.go#L411  
    data_source = https://github.com/hashicorp/terraform-provider-aws/blob/8e4d8a3f3f781b83f96217c2275f541c893fec5a/aws/provider.go#L169  
  
2.  
 - 	ConflictsWith: []string{"name_prefix"},  
         https://github.com/hashicorp/terraform-provider-aws/blob/8e4d8a3f3f781b83f96217c2275f541c893fec5a/aws/resource_aws_sqs_queue.go#L56  

 -  Длина строки не более 80  символов:  
         errors = append(errors, fmt.Errorf("%q cannot be longer than 80 characters", k))  
         https://github.com/hashicorp/terraform-provider-aws/blob/8e4d8a3f3f781b83f96217c2275f541c893fec5a/aws/validators.go#L1038  
 -  Регулярка : `^[0-9A-Za-z-_]+(\.fifo)?$` - может содержать только буквы и символы +".fofo" в конце  
                 есть еще 2 доп условия ниже по коду :   
                     NonFifo = `^[0-9A-Za-z-_]+$` - может содержать только буквы, цифры, подчеркиваниеы,   
                     Fifo = `^[0-9A-Za-z-_.]+$` - так же может содержать только буквы, цифры, подчеркивание, а так же точку,   
                            `^[^a-zA-Z0-9-_]` -  и при этом начинаться только с букв, цифр, подчеркивания,  
         https://github.com/hashicorp/terraform-provider-aws/blob/8e4d8a3f3f781b83f96217c2275f541c893fec5a/aws/validators.go#L1041  
