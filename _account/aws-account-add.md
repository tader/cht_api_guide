---
title: Enable AWS Account
position: 1
description: Enable an AWS Account in the CloudHealth Platform.
type: post
endpoint: https://chapi.cloudhealthtech.com/v1/aws_accounts
parameters:
  - name: name
    required: yes
    content: String that specifies the unique display name of an AWS account.
  - name: authentication
    required: yes
    content: JSON field that specifies how to authenticate with your AWS accounts. Use IAM Role (recommended) or IAM User (less secure) to authenticate.
    sub-fields:
      - name: protocol
        required: yes
        content: Authentication protocol. Specify `access_key` or `assume_role`
      - name: access_key
        required: yes, if `protocol == access_key`
        content: Access Key for IAM User
      - name: secret_key
        required: yes, if `protocol == access_key`
        content: Access Key for IAM User
      - name: assume_role
        required: yes, if `protocol == assume_role`
        content: Role ARN for IAM Role
      - name: assume_role_external_id
        required: yes, for IAM-Role-based authentication
        content: External ID generated by CloudHealth. See [How to get External ID](#accountexternal-id-get).
  - name: billing
    required: no
    content: JSON field that specifies the location of the AWS Detailed Billing Record (DBR) or the AWS Cost and Usage Report (CUR).
    sub-fields:
      - name: bucket
        required: yes
        content: Name of S3 bucket containing the DBR and CUR
  - name: cloudtrail
    required: no
    content: JSON field that specifies whether CloudHealth should collect CloudTrail Trails and the location of Trail files.
    sub-fields:
      - name: enabled
        required: yes
        content: Should CloudHealth collect CloudTrail trails? Default value is `False`
      - name: bucket
        required: yes
        content: Name of S3 bucket containing the files
      - name: prefix
        required: yes, if you have enabled prefixing in AWS
        content: Prefix of Trail files
  - name: aws_config
    required: no
    content: JSON field that specifies whether CloudHealth should collect AWS Config files and the location of the files.
    sub-fields:
      - name: enabled
        required: yes
        content: Should CloudHealth collect AWS Config files? Default value is `False`
      - name: bucket
        required: yes
        content: Name of S3 bucket containing the files
      - name: prefix
        required: yes, if you have enabled prefixing in AWS
        content: Prefix of files
  - name: cloudwatch
    required: no
    content: JSON field that specifies whether CloudHealth should collect CloudWatch data.
    sub-fields:
      - name: enabled
        required: yes
        content: Should CloudHealth collect AWS Config files? Default value is `True`
  - name: tags
    required: no
    content: JSON field that specifies key-value pairs for tags. When you use this field, The API restricts queries to AWS accounts that are tagged with these key-value pairs.
    sub-fields:
      - name: key
        required: yes
        content: Tag key
      - name: value
        required: yes
        content: Tag value
  - name: hide_public_fields
    required: no
    content: Boolean field that specifies whether CloudHealth should store public DNS and IP. Default value is `True`
  - name: region
    required: no
    content: JSON field that specifies the type of AWS Account. Value can be `global` (default) or `govcloud`.
content_markdown: |-
  Result header contains `Location: https://chapi.cloudhealthtech.com/v1/aws_accounts/1`
right_code_blocks:
  - code_block: |-
      {
        "name": "Production Account",
        "authentication": {
          "protocol": "access_key",
          "access_key": "AKIAQQQQQQQQQQQ",
          "secret_key": "S87345j34lkj3l45lkj+2342"
        },
        "billing": {
          "bucket": "my-billing-bucket"
        },
        "cloudtrail": {
          "enabled": true,
          "bucket": "my-cloudtrail-bucket"
        },
        "aws_config": {
          "enabled" :true,
          "bucket": "my-aws-config-bucket",
          "prefix": "foo"
        },
        "tags": [
          {"key": "Environment", "value": "Production"}
        ]
      }
    title: Request Body
    language: json
  - code_block: |-
      {
        "id": 1,
        "name": "Production Account",
        "hide_public_fields": false,
        "region": "global",
        "created_at": "2015-12-16T23:03:49Z",
        "updated_at": "2015-12-16T23:03:49Z",
        "account_type": "Unknown",
        "status": {
          "level": "unknown"
        },
        "authentication": {
          "protocol": "access_key",
          "access_key": "AKIAQQQQQQQQQQQ"
        },
        "billing": {
          "bucket": "my-billing-bucket",
          "is_consolidated": false
        },
        "cloudtrail": {
          "enabled": true,
          "bucket": "my-cloudtrail-bucket"
        },
        "aws_config": {
          "enabled": true,
          "bucket": "my-aws-config-bucket",
          "prefix": "foo"
        },
        "cloudwatch": {
          "enabled": true
        },
        "tags": [
        {
          "key": "Environment",
          "value": "production"
        }
        ],
        "_links": {
          "self": {
            "href": "/v1/aws_accounts/1"
          }
        }
      }
    title: Response Body
    language: json
  - code_block: |-
      curl -d
        '{
          "name": "Production Account",
          "authentication": {
            "protocol": "access_key",
            "access_key": "AKIAQQQQQQQQQQQ",
            "secret_key": "S87345j34lkj3l45lkj+2342"
          },
          "billing": {
            "bucket": "my-billing-bucket"
          },
          "cloudtrail": {
            "enabled": true,
            "bucket": "my-cloudtrail-bucket"
          },
          "aws_config": {
            "enabled" :true,
            "bucket": "my-aws-config-bucket",
            "prefix": "foo"
          },
          "tags": [{
            "key": "Environment",
            "value": "Production"
          }]
        }'
        -H 'Content-Type: application/json' --request POST 'https://chapi.cloudhealthtech.com/v1/aws_accounts?api_key=<your_api_key>'
    title: Sample Request
    language: bash
---
