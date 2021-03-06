---
layout: "alicloud"
page_title: "Alicloud: alicloud_launch_template"
sidebar_current: "docs-alicloud-resource-launch-tempate"
description: |-
  Provides an ECS Launch Template resource.
---

# alicloud\_launch\_template

Provides an ECS Launch Template resource.

For information about Launch Template and how to use it, see [Launch Template](https://www.alibabacloud.com/help/doc-detail/73916.html).

## Example Usage

```
data "alicloud_images" "images" {
    owners = "system"
}

data "alicloud_instances" "instances" {
}

resource "alicloud_launch_template" "template" {
    name = "tf-test-template"
    description = "test1"
    image_id = "${data.alicloud_images.images.images.0.id}"
    host_name = "tf-test-host"
    instance_charge_type = "PrePaid"
    instance_name = "tf-instance-name"
    instance_type = "${data.alicloud_instances.instances.instances.0.instance_type}"
    internet_charge_type = "PayByBandwidth"
    internet_max_bandwidth_in = 5
    internet_max_bandwidth_out = 0
    io_optimized = "none"
    key_pair_name = "test-key-pair"
    ram_role_name = "xxxxx"
    network_type = "vpc"
    security_enhancement_strategy = "Active"
    spot_price_limit = 5
    spot_strategy = "SpotWithPriceLimit"
    security_group_id = "sg-zxcvj0lasdf102350asdf9a"
    system_disk_category = "cloud_ssd"
    system_disk_description = "test disk"
    system_disk_name = "hello"
    system_disk_size = 40
    resource_group_id = "rg-zkdfjahg9zxncv0"
    userdata = "xxxxxxxxxxxxxx"
    vswitch_id = "sw-ljkngaksdjfj0nnasdf"
    vpc_id = "vpc-asdfnbg0as8dfk1nb2"
    zone_id = "beijing-a"

    tags = {
        tag1 = "hello"
        tag2 = "world"
    }
    network_interfaces = [
        {
            name = "eth0"
            description = "hello1"
            primary_ip = "10.0.0.2"
            security_group_id = "xxxx"
            vswitch_id = "xxxxxxx"
        }
    ]
    data_disks = [
        {
            name = "disk1"
            description = "test1"
        },
        {
            name = "disk2"
            description = "test2"
        }
    ]
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Optional, ForceNew) Instance launch template name. Can contain [2, 128] characters in length. It must start with an English letter (uppercase or lowercase) and can contain numbers, periods (.), colons (:), underscores (_), and hyphens (-). It cannot start with "http://" or "https://".
* `description` - (Optional, ForceNew) Description of instance launch template version 1. It can be [2, 256] characters in length. It cannot start with "http://" or "https://". The default value is null.
* `host_name` - (Optional, ForceNew) Instance host name.It cannot start or end with a period (.) or a hyphen (-) and it cannot have two or more consecutive periods (.) or hyphens (-).For Windows: The host name can be [2, 15] characters in length. It can contain A-Z, a-z, numbers, periods (.), and hyphens (-). It cannot only contain numbers. For other operating systems: The host name can be [2, 64] characters in length. It can be segments separated by periods (.). It can contain A-Z, a-z, numbers, and hyphens (-).
* `image_id` - (Optional, ForceNew) Image ID.
* `instance_name` - (Optional, ForceNew) The name of the instance. The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods (.), colons (:), underscores (_), and hyphens (-).
* `instance_charge_type` - (Optional, ForceNew)Billing methods. Optional values:
    - PrePaid: Monthly, or annual subscription. Make sure that your registered credit card is invalid or you have insufficient balance in your PayPal account. Otherwise, InvalidPayMethod error may occur.
    - PostPaid: Pay-As-You-Go.

    Default value: PostPaid.
* `instance_type` - (Optional, ForceNew) Instance type. For more information, call resource_alicloud_instances to obtain the latest instance type list.
* `auto_release_time` - (Optional, ForceNew) Instance auto release time. The time is presented using the ISO8601 standard and in UTC time. The format is  YYYY-MM-DDTHH:MM:SSZ.
* `internet_charge_type` - (Optional, ForceNew) Internet bandwidth billing method. Optional values: PayByTraffic.
* `internet_max_bandwidth_in` - (Optional, ForceNew) The maximum inbound bandwidth from the Internet network, measured in Mbit/s. Value range: [1, 200].
* `internet_max_bandwidth_out` - (Optional, ForceNew) Maximum outbound bandwidth from the Internet, its unit of measurement is Mbit/s. Value range: [0, 100].
* `io_optimized` - (Optional, ForceNew) Whether it is an I/O-optimized instance or not. Optional values:
    - none
    - optimized
* `key_pair_name` - (Optional, ForceNew) The name of the key pair.
    - Ignore this parameter for Windows instances. It is null by default. Even if you enter this parameter, only the  Password content is used.
    - The password logon method for Linux instances is set to forbidden upon initialization.
* `network_type` - (Optional, ForceNew) Network type of the instance. Value options: Classic | VPC.
* `ram_role_name` - (Optional, ForceNew) The RAM role name of the instance. You can use the RAM API ListRoles to query instance RAM role names.
* `security_enhancement_strategy` - (Optional, ForceNew) Whether or not to activate the security enhancement feature and install network security software free of charge. Optional values: Active | Deactive.
* `security_group_id` - (Optional, ForceNew) The security group ID.
* `spot_price_limit` -(Optional, ForceNew) 	Sets the maximum hourly instance price. Supports up to three decimal places.
* `spot_strategy` - (Optional, ForceNew) The spot strategy for a Pay-As-You-Go instance. This parameter is valid and required only when InstanceChargeType is set to PostPaid. Value range:
    - NoSpot: Normal Pay-As-You-Go instance.
    - SpotWithPriceLimit: Sets the maximum price for a spot instance.
    - SpotAsPriceGo: The system automatically calculates the price. The maximum value is the Pay-As-You-Go price.
* `system_disk_category` - (Optional, ForceNew) The category of the system disk. System disk type. Optional values:
    - Cloud: Basic cloud disk.
    - cloud_efficiency: Ultra cloud disk.
    - cloud_ssd: SSD Cloud Disks.
    - ephemeral_ssd: Ephemeral SSD.
* `system_disk_description` - (Optional, ForceNew) System disk description. It cannot begin with http:// or https://.
* `system_disk_name` - (Optional, ForceNew) System disk name. The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods (.), colons (:), underscores (_), and hyphens (-).
* `system_disk_size` - (Optional, ForceNew) Size of the system disk, measured in GB. Value range: [20, 500].
* `userdata` - (Optional, ForceNew) User data of the instance, which is Base64-encoded. Size of the raw data cannot exceed 16 KB.
* `vswitch_id` - (Optional, ForceNew) When creating a VPC-Connected instance, you must specify its VSwitch ID.
* `zone_id` - (Optional, ForceNew) The zone ID of the instance.
* `network_interfaces` - (Optional, ForceNew) The list of network interfaces created with instance.
    * `name` - (Optional, ForceNew) ENI name.
    * `description` - (Optional, ForceNew) The ENI description.
    * `primary_ip` - (Optional, ForceNew) The primary private IP address of the ENI.
    * `security_group_id` - (Optional, ForceNew) The security group ID must be one in the same VPC.
    * `vswitch_id` - (Optional, ForceNew) The VSwitch ID for ENI. The instance must be in the same zone of the same VPC network as the ENI, but they may belong to different VSwitches.
* `data_disks` - (Optional, ForceNew) The list of data disks created with instance.
    * `name` - (Optional, Force New) The name of the data disk.
    * `size` - (Required, Force New) The size of the data disk.
        - cloud：[5, 2000]
        - cloud_efficiency：[20, 32768]
        - cloud_ssd：[20, 32768]
        - ephemeral_ssd：[5, 800]
    * `category` - (Optional, Force New) The category of the disk:
        - `cloud`: The general cloud disk.
        - `cloud_efficiency`: The efficiency cloud disk.
        - `cloud_ssd`: The SSD cloud disk.
        - `ephemeral_ssd`: The local SSD disk.

        Default to `cloud_efficiency`.
    * `encrypted` -(Optional, Bool, Force New) Encrypted the data in this disk.

        Default to false
    * `snapshot_id` - (Optional, Force New) The snapshot ID used to initialize the data disk. If the size specified by snapshot is greater that the size of the disk, use the size specified by snapshot as the size of the data disk.
    * `delete_with_instance` - (Optional, Force New) Delete this data disk when the instance is destroyed. It only works on cloud, cloud_efficiency and cloud_ssd disk. If the category of this data disk was ephemeral_ssd, please don't set this param.

        Default to true
    * `description` - (Optional, Force New) The description of the data disk.
* `tags` - (Optional, ForceNew) A mapping of tags to assign to the resource.
    - Key: It can be up to 64 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://". It cannot be a null string.
    - Value: It can be up to 128 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://". It can be a null string.
            
            
            
## Attributes Reference

The following attributes are exported:

* `id` - The Launch Template ID.

## Import

Launch Template can be imported using the id, e.g.

```
$ terraform import alicloud_launch_template.lt lt-abc1234567890000
```
