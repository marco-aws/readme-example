# Some meaningful title

_one line description of the content_

## Pre-reqs

* Terraform version 12345
* AWS credentials configured via CLI 
* Etc. etc.

## Setup 

* 1: update the variables in the log2splunk.tf file:

* 2: update `provider.tf` file (set deployment region, and aws credentials if needed)

* 3: initiate deployement (terraform init/plan/apply) from the directory containing `log2splunk.tf` file

* 4: The CloudWatch logs destination ARN is provided as output of the configuration. Use this ARN to setup cross-account subscription filters on the desired log group, with the desired filtering pattern.

## Variables

| **Name**             | **Description**                                    | **Default**    |
|----------------------|----------------------------------------------------|----------------|
| region               | deployment region                                  | `eu-central-1` |
| logging_account_list | list of accounts authorized to ship logs to Splunk | `[]`           |
| hec_token            | token of Splunk HEC Endpoint.                      | -              |
| hec_url              | complete URL (with port) of HEC endpoint           | -              |

## Example:

```
module "kinesis_firehose" {
  source = "./log2splunk"
  region = "ap-northeast-1"
  logging_account_list = ["123456789012","234567890123","345678901234"]
  hec_token = "1fac374d-220f-43f1-92d5-12345631f253"
  hec_url = "https://http-inputs-flatiron-jp.splunkcloud.com/services/collector/event"
  s3_bucket_name = "fh-log-spillbucket-3497f973"
}
```

### Acknowledgements for original artifact:

_(c) 2022 Amazon Web Services, Inc. or its affiliates. All Rights Reserved. This AWS Content is provided subject to the terms of the AWS Customer Agreement available at http://aws.amazon.com/agreement (http://aws.amazon.com/agreement) or other written agreement between Customer and either Amazon Web Services, Inc. or Amazon Web Services EMEA SARL or both._
