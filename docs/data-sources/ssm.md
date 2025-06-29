---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "tunnel_ssm Data Source - tunnel"
subcategory: ""
description: |-
  Create a local AWS SSM tunnel to a remote host
---

# tunnel_ssm (Data Source)

Create a local AWS SSM tunnel to a remote host

## Example Usage

```terraform
# The following example shows how to create a tunnel for an AWS RDS database.

data "tunnel_ssm" "rds" {
  target_host  = "https://my-db.us-east-1.rds.amazonaws.com"
  target_port  = 443
  ssm_instance = "i-instanceid"
  ssm_region   = "us-east-1"
}

provider "postgresql" {
  host     = data.tunnel_ssm.rds.local_host
  port     = data.tunnel_ssm.rds.local_port
  database = "my-database"
  username = "my-user"
  password = "my-password"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `ssm_instance` (String) Specify the exact Instance ID of the managed node to connect to for the session
- `target_host` (String) The DNS name or IP address of the remote host
- `target_port` (Number) The port number of the remote host

### Optional

- `ssm_profile` (String) AWS profile name as set in credentials files. Can also be set using either the environment variables `AWS_PROFILE` or `AWS_DEFAULT_PROFILE`.
- `ssm_region` (String) AWS Region where the instance is located. The Region must be set. Can also be set using either the environment variables `AWS_REGION` or `AWS_DEFAULT_REGION`.
- `ssm_role_arn` (String) ARN of an IAM role to assume.

### Read-Only

- `local_host` (String) The DNS name or IP address of the local host
- `local_port` (Number) The local port number to use for the tunnel
