---
layout: "alicloud"
page_title: "Alicloud: alicloud_kvstore_instances"
sidebar_current: "docs-alicloud-datasource-kvstore-instances"
description: |-
    Provides a collection of kvstore instances according to the specified filters.
---

# alicloud\_kvstore\_instances

This data source provides a collection of kvstore instances available in an Alibaba Cloud account.
Filters support searches by instance name, searches by tags, and other filters.

## Example

```
data "alicloud_kvstore_instances" "dbs" {
  name_regex = "data-\\d+"
  status     = "Running"
  tags       = <<EOF
{
  "type": "cache",
  "size": "small"
}
EOF
}
```

## Argument Reference

The following arguments are supported:

* `name_regex` - (Optional) Apply a regex string to the instance name.
* `instance_type` - (Optional) Filter by database type. Options are `Memcache`, and `Redis`. 
* `status` - (Optional) Filter by status of the instance.
* `instance_class`- (Optional) Filter by type of the applied ApsaraDB for Redis instance.
For more information, see [Instance type table](https://www.alibabacloud.com/help/doc-detail/61135.htm).
* `vpc_id` - (Optional) Retrieve instances that belong to specified VPC.
* `vswitch_id` - (Optional) Retrieve instances that belong to specified `vswitch` resources.
* `tags` - (Optional) Query the instance bound to the tag. The format of the incoming value is `json` string, including `TagKey` and `TagValue`. `TagKey` cannot be null, and `TagValue` can be empty. Format example: `{"key1":"value1"}`.
* `output_file` - (Optional) Set the name of file where the collection of instances will be saved after running `terraform plan`.

## Attributes Reference

The following attributes are returned in addition to the arguments listed above:

* `instances` - A list of RDS instances. Every element contains the following attributes:
  * `id` - The ID of the RKV instance.
  * `name` - The name of the RDS instance.
  * `charge_type` - Billing method. Possible values: `PostPaid` for  Pay-As-You-Go and `PrePaid` for subscription.
  * `region_id` - Region ID the instance belongs to.
  * `create_time` - Creation time of the instance.
  * `expire_time` - Expiration time. Pay-As-You-Go instances are never expire.
  * `status` - Status of the instance.
  * `instance_type` - (Optional) Database type. Options are `Memcache`, and `Redis`. If no value is specified, all types are returned.
  * `instance_class`- (Optional) Type of the applied ApsaraDB for Redis instance.
  For more information, see [Instance type table](https://www.alibabacloud.com/help/doc-detail/61135.htm).
  * `availability_zone` - Availability zone.
  * `vpc_id` - VPC ID the instance belongs to.
  * `vswitch_id` - VSwitch ID the instance belongs to.
  * `private_ip` - Private IP address of the instance.
  * `username` - The username of the instance.
  * `capacity` - Capacity of the applied ApsaraDB for Redis instance. Unit: MB.
  * `bandwidth` - Instance bandwidth limit. Unit: Mbit/s.
  * `connections` - Instance connection quantity limit. Unit: count.
  * `connections_domain` - Instance connection domain (only Intranet access supported).
  * `port` - Connection port of the instance.
  