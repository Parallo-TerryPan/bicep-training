# Overview
This section is an introduction into Bicep basics.  
To get a background understanding of Bicep, read:
- [What is Bicep?](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview?tabs=bicep)

Follow the sections below to complete `Part 1`

# Bicep: Best Practices
Here are coding values we want you to approach the following sections with:
* `parameters`, `variables` and value names should be written in `camelCase` format. Example: `var appServiceName = 'myappservicename'` - lowercase start, with no spaces between words, a captial letter denotes the next word.
* For bicep, try to use as few `parameters` (where you get to choose) as possible, with the majority of definition occuring at the `variable` level.
* secrets should never be stored in plain text. Please store secrets in Azure Key Vaults first, second option is to use Variable Groups (in ADO).
* `variables` in bicep are values specific to that level of code - so in a module these are values that conditionally change based on a parameter, or a just values for the resource in the module. They are ways to isolate values that may need changing later. Any values that are very unlikely to change over time (e.g. TLS level in a database) can be hard-coded into templates.
* if you want a default state, use `parameter` defaults. These values can be overridden to use desired states. This is preferable to creating multiple similar files, as those quickly become hard to manage.
* ensure formatting is correct when write code - the indentation and spaces between code should be uniform/as documentation shows. This makes for clean code that is easier to read and troubleshoot.


# Create a new branch
Tasks:
1. In your __local__ repository, create a new branch called `part-1`, based on `main`
1. Push this branch to your __remote__ repository

# Create a main bicep file
Required Reading: 
- [Bicep file](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/file)
- [Parameters (param)](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/parameters)
- [Variables (var)](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/variables)

Tasks:  
1. In your new branch, create a folder called `bicep`
1. Create a new file called `main.bicep`
1. Create basic parameters directly inside `main.bicep`
    ```
    Parameters values to create:
        workloadPrefix - '<your three letter initial>'
        environmentCode - 'test'
        location - '<resource group location>' - e.g. 'australiaeast'
        locationCode - '<short hand code for location> e.g. code = 'ae' if you region is australia east'
    ```
    To get `location` value, you can run the following CLI command: `az account list-locations`
1. Commit your code with an informative message

# Create your first resource in Bicep - storage account
[Storage Account - Bicep](https://learn.microsoft.com/en-us/azure/templates/microsoft.storage/storageaccounts?pivots=deployment-language-bicep)

Tasks:  
1. Within `main.bicep`, create a variable for storage account name  
    Build the value using the parameters you created in the section above
    ```
    var storageAccountName = 'sa${workloadPrefix}${environmentCode}${locationCode}'
    ``` 
    _Note: `${}` is the way to reference parameters/variables within bicep when creating a `string`_

1. Within `main.bicep`, create a storage account resource in bicep format.  
    These are the required properties for the storage account:

    ```
    resource name: 'storageAccount'  
    storage account name: variable for storage account name  
    location: location parameter
    kind: 'StorageV2'  
    sku name: 'Standard_LRS'  
    allowBlobPublicAccess: true  
    accessTier: 'Hot'  
    minimumTlsVersion: 'TLS1_2'
    publicNetworkAccess: 'Enabled'  
    networkAcls: {
        bypass: 'AzureServices'
        defaultAction: 'Allow'
        ipRules: []
        virtualNetworkRules: []
    }
    supportsHttpsTrafficOnly: true
    ```
    *The code above is pseudo code. It will not work if you copy and paste directly to your bicep file.*
1. Change your code to make the values within the storage account resource into variables and reference them in code  
    An example of this:  
    `var minimumTlsVersion = 'TLS1_2'`  
    You can now use the variable `minimumTlsVersion` in the storage account resource value - `minimumTlsVersion: minimumTlsVersion` - instead of hard-coding the value, adding flexibility
1. Commit your code with an informative message

Optional Reading: 
- [Bicep file](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/file)
- [Storage account documentation](https://learn.microsoft.com/en-us/azure/templates/microsoft.storage/storageaccounts?pivots=deployment-language-bicep)

# Deploy resources to a resource group using CLI
Tasks:
1. In your local terminal, start a new session. Connect your Azure tenant using az cli  
(__Note: Azure CLI will need to be installed on your local machine__)
1. Set the subscription context to your subscription within the tenancy (`az account set`)
1. Create the resource group via CLI
    * Create your resource group with name `rg-{workloadPrefix}-{environmentCode}-{locationCode}` 
1. Deploy your local bicep file to Azure from command line, at resource group scope
    * Deployment name - `firstDeployment`
1. Go to Azure and view your deployment


Optional Reading: 
- [How to install the Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- [Manage subscriptions](https://learn.microsoft.com/en-us/cli/azure/manage-azure-subscriptions-azure-cli)
- [Use deployment templates](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/deploy-cli?toc=%2Fcli%2Fazure%2Ftoc.json&bc=%2Fcli%2Fazure%2Fbreadcrumb%2Ftoc.json)
- [View deployment history](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/deployment-history?tabs=azure-portal)
- [Scopes - Resource Groups](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/deploy-to-resource-group?tabs=azure-cli)

# Create a Bicep parameters file
Required Reading:
- [Parameters file](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/parameter-files?tabs=Bicep)

Tasks:
1. In the same directory as `main.bicep`, create Bicep parameters file `main.bicepparam`
1. Link this file to `main.bicep` file
1. Set parameter values in the new file, remove hard-coded parameter values (aside from location) in `main.bicep`
1. Commit your code with an informative message

## Troubleshooting using Azure Portal
In the Azure Portal, you can view your deployments by navigating to the deployments window in a subscription or a resource group. This view is very helpful when troubleshooting a deployment.

## --what-if argument
During a deployment, we can use the `--what-if` argument during a deployment to perform a dry run. This will show the changes that will be applied when the deployment is run.
```
az deployment group create -g <resourceGroupName> --template-file main.bicep --parameters main.bicepparam --what-if
``` 

# Completion
You have made it to the end of `Part 1`, nice work! 

1. Create a pull request against your `main` branch to commit your branch changes.
1. Take screenshots of the following in Azure and add to your pull request overview
    * the resource group you created
    * the deployment overview in Azure
1. Set your pull request to `auto-complete`. Select the following for post-completion  
    - Merge type: Merge (no fast forward)
    - Select: Delete `branch name` after merging
    - Leave other options unselected

Your mentor will review your work and reach out to you.

Once you have confirmation from your mentor, you can start `Part 2`. 