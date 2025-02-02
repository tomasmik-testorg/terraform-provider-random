---

<!-- Please do not edit this file, it is generated. -->
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "random_id Resource - terraform-provider-random"
subcategory: ""
description: |-
  The resource random_id generates random numbers that are intended to be
  used as unique identifiers for other resources.
  This resource does use a cryptographic random number generator in order
  to minimize the chance of collisions, making the results of this resource
  when a 16-byte identifier is requested of equivalent uniqueness to a
  type-4 UUID.
  This resource can be used in conjunction with resources that have
  the create_before_destroy lifecycle flag set to avoid conflicts with
  unique names during the brief period where both the old and new resources
  exist concurrently.
---

# random_id (Resource)

The resource `randomId` generates random numbers that are intended to be
used as unique identifiers for other resources.

This resource *does* use a cryptographic random number generator in order
to minimize the chance of collisions, making the results of this resource
when a 16-byte identifier is requested of equivalent uniqueness to a
type-4 UUID.

This resource can be used in conjunction with resources that have
the `createBeforeDestroy` lifecycle flag set to avoid conflicts with
unique names during the brief period where both the old and new resources
exist concurrently.

## Example Usage

```typescript
// DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { Fn, Token, TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { Instance } from "./.gen/providers/aws/instance";
import { Id } from "./.gen/providers/random/id";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    const server = new Id(this, "server", {
      byteLength: 8,
      keepers: {
        ami_id: amiId.stringValue,
      },
    });
    const awsInstanceServer = new Instance(this, "server_1", {
      ami: Token.asString(Fn.lookupNested(server, ["keepers", "ami_id"])),
      tags: {
        Name: "web-server ${" + server.hex + "}",
      },
    });
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    awsInstanceServer.overrideLogicalId("server");
  }
}

```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `byteLength` (Number) The number of random bytes to produce. The minimum value is 1, which produces eight bits of randomness.

### Optional

- `keepers` (Map of String) Arbitrary map of values that, when changed, will trigger recreation of resource. See [the main provider documentation](../index.html) for more information.
- `prefix` (String) Arbitrary string to prefix the output value with. This string is supplied as-is, meaning it is not guaranteed to be URL-safe or base64 encoded.

### Read-Only

- `b64Std` (String) The generated id presented in base64 without additional transformations.
- `b64Url` (String) The generated id presented in base64, using the URL-friendly character set: case-sensitive letters, digits and the characters `_` and `-`.
- `dec` (String) The generated id presented in non-padded decimal digits.
- `hex` (String) The generated id presented in padded hexadecimal digits. This result will always be twice as long as the requested byte length.
- `id` (String) The generated id presented in base64 without additional transformations or prefix.

## Import

Import is supported using the following syntax:

```shell
# Random IDs can be imported using the b64_url with an optional prefix. This
# can be used to replace a config value with a value interpolated from the
# random provider without experiencing diffs.

# Example with no prefix:
terraform import random_id.server p-9hUg

# Example with prefix (prefix is separated by a ,):
$ terraform import random_id.server my-prefix-,p-9hUg
```

<!-- cache-key: cdktf-0.19.0 input-0fb181c93bbdaa572d25c9a75fb79bf8bbc7e3d3f03383b3e56860208d55a253 556251879b8ed0dc4c87a76b568667e0ab5e2c46efdd14a05c556daf05678783-->