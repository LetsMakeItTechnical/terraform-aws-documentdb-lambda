
# terraform-aws-documentdb-lambda

>
## create resources on AWS:
```bash
#
$ export AWS_ACCESS_KEY_ID=<YOUR_AWS_ACCESS_KEY_ID>
$ export AWS_SECRET_ACCESS_KEY=<YOUR_AWS_SECRET_ACCESS_KEY>

# set variable as env vars or in vars.tf file
$ export TF_VAR_name=<NAME_FOR_RESOURCES> # by default geek_api
$ export TF_VAR_docdb_password=<PASSWORD_FOR_AMAZON_DOCUMENTDB>
# if you have a domain on AWS
# lambda will be available at https://<TF_VAR_name>.<TF_VAR_main_domain>
$ export TF_VAR_certificate_arn=<YOUR_DOMAIN_SERTIFICATE_ARN>
$ export TF_VAR_zone_id=Z1NT1BON8JUIVM=<YOUR_DOMAIN_ZONE_ID>
$ export TF_VAR_main_domain=<YOUR_DOMAIN>

$ terraform init
$ terraform apply
```

## Outputs:
 - aws_instance_public_dns
 - url
 - docdb_endpoint
 - docdb_username
 - bucket
 - bucket_key
 - name

## Connect to Amazon DocumentDB
```bash
$ ssh -i tf-<var.name>-ec2 ubuntu<aws_instance_public_dns>
$ mongo \
  --host <docdb_endpoint> \
  --username <docdb_username> \
  --password <var.docdb_password>
```

## update function code:
```bash
$ export AWS_DEFAULT_REGION=<var.region>
$ aws s3 cp lambda.zip s3://<bucket>/<bucket_key>
$ aws lambda update-function-code --function-name tf-<var.name> --s3-bucket <bucket> --s3-key <bucket_key>
```

## License
