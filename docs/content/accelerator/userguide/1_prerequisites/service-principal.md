---
title: Authenticating via Service Principal
weight: 100
---

## Authenticate via Service Principal

Skip this if using a User account as recommended.

### Create Service Principal

1. Navigate to the [Azure Portal](https://portal.azure.com) and sign in to your tenant.
1. Search for `Entra ID` and open it.
1. Copy the `Tenant ID` field and save it somewhere safe, making a note it is the `ARM_TENANT_ID`.
1. Click `App registrations` in the left navigation.
1. Click `+ New registration`.
1. Choose a name (SPN) that you will remember and make a note of it, we recommend using `sp-alz-bootstrap`.
1. Type the chosen name into the `Name` field.
1. Leave the other settings as default and click `Register`.
1. Wait for it to be created.
1. Copy the `Application (client) ID` field and save it somewhere safe, making a note it is the `ARM_CLIENT_ID`.
1. Click `Certificates & secrets` in the left navigation.
1. Ensure the `Client secrets` tab is selected and click `+ New client secret`.
1. Enter `ALZ Bootstrap` in the `Description` field.
1. Change the `Expires` field, choose `Custom`.
1. Set the `Start` field to todays date.
1. Set the `End` field to tomorrows date.
1. Click `Add`.
1. Copy the `Value` field save it somewhere safe, making a note that it is the `ARM_CLIENT_SECRET`.

### Create Permissions

1. The service principal name (SPN) is the username of the User account or the name of the app registration you created.
1. Search for `Subscriptions` and click to navigate to the subscription view.
1. For each of the subscriptions you created in the previous step:
    1. Navigate to the subscription.
    1. Click `Access control (IAM)` in the left navigation.
    1. Click `+ Add` and choose `Add role assignment`.
    1. Choose the `Privileged administrator roles` tab.
    1. Click `Owner` to highlight the row and then click `Next`.
    1. Leave the `User, group or service principal` option checked.
    1. Click `+ Select Members` and search for your SPN in the search box on the right.
    1. Click on your User to highlight it and then click `Select` and then click `Next`.
    1. Click the `Allow user to assign all roles (highly privileged)` option.
    1. Click `Review + assign`, then click `Review + assign` again when the warning appears.
    1. Wait for the role to be assigned and move onto the next subscription.
1. Search for `Management Groups` and click to navigate to the management groups view.
1. Click the parent management group you plan to deploy the Landing Zone into (this could be `Tenant Root Group` or a new management group you created).
1. Click `Access control (IAM)` in the left navigation.
1. Click `+ Add` and choose `Add role assignment`.
1. Choose the `Privileged administrator roles` tab.
1. Click `Owner` to highlight the row and then click `Next`.
1. Click `Next`.
1. Leave the `User, group or service principal` option checked.
1. Click `+ Select Members` and search for your SPN in the search box on the right.
1. Click on your User to highlight it and then click `Select`.
1. Click `Review + assign`, then click `Review + assign` again when the warning appears.
1. Wait for the role to be assigned and you are done with this part.

### Set Service Principal Credentials in Terminal

1. Open a new PowerShell Core (pwsh) terminal.
1. Find the `ARM_TENANT_ID` you made a note of earlier.
1. Type `$env:ARM_TENANT_ID="<tenant id>"` and hit enter.
1. Find the `ARM_CLIENT_ID` you made a note of earlier.
1. Type `$env:ARM_CLIENT_ID="<client id>"` and hit enter.
1. Find the `ARM_CLIENT_SECRET` you made a note of earlier.
1. Type `$env:ARM_CLIENT_SECRET="<client id>"` and hit enter.
1. Find the subscription id of the management subscription you made a note of earlier.
1. Type `$env:ARM_SUBSCRIPTION_ID="<subscription id>"` and hit enter.

{{< hint type=note >}}
If you close your PowerShell prompt prior to running the bootstrap, you need to re-enter these environment variables.
{{< /hint >}}

## Next Steps

Return to [Phase 1]({{< relref "1_prerequisites" >}}) step **version control systems**.
