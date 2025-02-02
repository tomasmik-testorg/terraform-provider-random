---

<!-- Please do not edit this file, it is generated. -->
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "random_pet Resource - terraform-provider-random"
subcategory: ""
description: |-
  The resource random_pet generates random pet names that are intended to be used as unique identifiers for other resources.
  This resource can be used in conjunction with resources that have the create_before_destroy lifecycle flag set, to avoid conflicts with unique names during the brief period where both the old and new resources exist concurrently.
---

# random_pet (Resource)

The resource `randomPet` generates random pet names that are intended to be used as unique identifiers for other resources.

This resource can be used in conjunction with resources that have the `createBeforeDestroy` lifecycle flag set, to avoid conflicts with unique names during the brief period where both the old and new resources exist concurrently.

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
import { Pet } from "./.gen/providers/random/pet";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    const server = new Pet(this, "server", {
      keepers: {
        ami_id: amiId.stringValue,
      },
    });
    const awsInstanceServer = new Instance(this, "server_1", {
      ami: Token.asString(Fn.lookupNested(server, ["keepers", "ami_id"])),
      tags: {
        Name: "web-server-${" + server.id + "}",
      },
    });
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    awsInstanceServer.overrideLogicalId("server");
  }
}

```

<!-- schema generated by tfplugindocs -->
## Schema

### Optional

- `keepers` (Map of String) Arbitrary map of values that, when changed, will trigger recreation of resource. See [the main provider documentation](../index.html) for more information.
- `length` (Number) The length (in words) of the pet name. Defaults to 2
- `prefix` (String) A string to prefix the name with.
- `separator` (String) The character to separate words in the pet name. Defaults to "-"

### Read-Only

- `id` (String) The random pet name.

<!-- cache-key: cdktf-0.19.0 input-6817a99fd74086b883ff0596b3649d0f6a3dcaab94e9dea42308adc5fa0fada5 556251879b8ed0dc4c87a76b568667e0ab5e2c46efdd14a05c556daf05678783-->