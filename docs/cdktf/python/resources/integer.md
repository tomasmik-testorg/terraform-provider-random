---

<!-- Please do not edit this file, it is generated. -->
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "random_integer Resource - terraform-provider-random"
subcategory: ""
description: |-
  The resource random_integer generates random values from a given range, described by the min and max attributes of a given resource.
  This resource can be used in conjunction with resources that have the create_before_destroy lifecycle flag set, to avoid conflicts with unique names during the brief period where both the old and new resources exist concurrently.
---

# random_integer (Resource)

The resource `random_integer` generates random values from a given range, described by the `min` and `max` attributes of a given resource.

This resource can be used in conjunction with resources that have the `create_before_destroy` lifecycle flag set, to avoid conflicts with unique names during the brief period where both the old and new resources exist concurrently.

## Example Usage

```python
# DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
from constructs import Construct
from cdktf import Fn, Token, TerraformStack
#
# Provider bindings are generated by running `cdktf get`.
# See https://cdk.tf/provider-generation for more details.
#
from imports.aws.alb_listener_rule import AlbListenerRule
from imports.random.integer import Integer
class MyConvertedCode(TerraformStack):
    def __init__(self, scope, name, *, condition):
        super().__init__(scope, name)
        priority = Integer(self, "priority",
            keepers={
                "listener_arn": listener_arn.string_value
            },
            max=50000,
            min=1
        )
        AlbListenerRule(self, "main",
            action=[AlbListenerRuleAction(
                target_group_arn=target_group_arn.string_value,
                type="forward"
            )
            ],
            listener_arn=Token.as_string(
                Fn.lookup_nested(priority, ["keepers", "listener_arn"])),
            priority=priority.result,
            condition=condition
        )
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `max` (Number) The maximum inclusive value of the range.
- `min` (Number) The minimum inclusive value of the range.

### Optional

- `keepers` (Map of String) Arbitrary map of values that, when changed, will trigger recreation of resource. See [the main provider documentation](../index.html) for more information.
- `seed` (String) A custom seed to always produce the same value.

### Read-Only

- `id` (String) The string representation of the integer result.
- `result` (Number) The random integer result.

## Import

Import is supported using the following syntax:

```shell
# Random integers can be imported using the result, min, and max, with an
# optional seed. This can be used to replace a config value with a value
# interpolated from the random provider without experiencing diffs.

# Example (values are separated by a ,):
terraform import random_integer.priority 15390,1,50000
```

<!-- cache-key: cdktf-0.19.0 input-14468c71f20ebc7d2a161542108e1cc214b9ae4d6f2c5008aa55d67bf9354ebf 556251879b8ed0dc4c87a76b568667e0ab5e2c46efdd14a05c556daf05678783-->