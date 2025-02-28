---
title: Modifying the Management Group Hierarchy
weight: 10
---

{{< hint type=important >}}
You will need to have a [custom library]({{< relref "customLibrary" >}}) if you want to modify the management group hierarchy.
Make sure you have completed that step before continuing.
{{< /hint >}}

To modify the management group hierarchy you can declare your own [alz_architecture_definition](https://azure.github.io/Azure-Landing-Zones-Library/assets/architectures/) file in your custom library.
This file can be in either YAML or JSON format.

Here is an example architecture definition file in YAML format:

```yaml
name: my custom architecture
management_groups:
  - id: my-root
    display_name: My Oaganizational Root Management Group
    archetypes:
      - root
    parent_id: null # this means that the mg will be created at the parent as defined in the module configuration.
    exists: false
  - id: my-landingzones
    display_name: My Landing Zones Management Group
    archetypes:
      - landing_zones
    parent_id: my-root
    exists: false
```

The above architecture would create two management groups, `my-root` and `my-landingzones`, with the `root` and `landing_zones` archetypes respectively.
You must define the entire hierarchy in your architecture definition file.

## Renaming Management Groups

To rename a management groups, please copy the default ALZ architecture definition from the [Library](https://github.com/Azure/Azure-Landing-Zones-Library/tree/main/platform/alz/architecture_definitions) into your local library.

Then we recommend that you change the value of the `name` field to something unique, this will help you identify your custom architecture definition.

Then you can rename the management groups as you wish.

Finally, in your ALZ module configuration, you can specify the `architecture_definition` variable to point to your custom architecture definition.

```terraform
module "alz" {
  source  = "Azure/avm-ptn-alz/azurerm"
  version = "~> 0.10"

  architecture_name = "my custom architecture"

  # other variable inputs...
}
```
