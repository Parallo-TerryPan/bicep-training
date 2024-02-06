# Pre-requisities
## Expected Knowledge
We expect before starting the sessions, you should know:
* General knowledge across Azure resources, familiar with core services via the portal
* Aware of Infrastructure-as-Code as a concept
* Aware of Azure DevOps and what it is generally used for
* Aware of DevOps as a concept
* Have worked with scripts in the past and understand basic concepts in scripting (e.g. parameters, variables, commands)
* Aware of Git and its general use case

## Azure CLI

You will need to install the [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) and [Azure Bicep tools](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/install).

## Visual Studio Code
If you don't already have VSCode installed, you should install VSCode to use as your Code editor, unless you already have another preferred editor.

[Download VSCode here](https://code.visualstudio.com/download)

### Handy extensions
This editor allows you to access extensions which make working with code easier and more user-friendly. Some extensions you may want to download are:
* Bicep
* Yaml
* Powershell
* Azure CLI Tools
* Azure Resource Manage (ARM) Tools


## Subscription setup
### Visual studio subscription

For the following workshop sessions, we need to ensure we have full tenant level control.

Tasks: 
1. Setup your personal Visual Studio Enterprise subscription in your own Azure Tenant

There are two ways to do this, depending on the current status of your subscription

1. Your Visual Studio Enterprise subscription is __not activated__  
    1. Go to https://my.visualstudio.com/, sign in with your work account (whichever has the license on it)
    2. Under `Benefits`, click _Activate_ 
    3. Use a personal hotmail account as Account Administrator, complete the tenant setup

2. Your Visual Studio Enterprise subscription is __activated__ and in an existing tenant (e.g. Contoso's)
    1. In Contoso tenant, go to `Azure Active Directory > Manage tenants > Create a new tenant` (this tenant will be your personal tenant, so name it what you would like)
    2. Once the new tenant has been created, go to your VS Studio Enterprise subscription in the tenant
    3. At the top of the subscription window in the portal, change your subscriptions directory - select the new personal tenant you have just created
    4. Once your subscription has been moved across to your new tenant, you will be able to see it by logging into your tenant
    5. Invite your personal hotmail account to the tenant via AAD and assign it the Global Administrator role

You will now be able to complete the following sessions when tenant level resources/changes are created/required.

Documentation: 
- [Create a Directory](https://learn.microsoft.com/en-nz/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)
- [Associate an Azure subscription](https://learn.microsoft.com/en-nz/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory)


