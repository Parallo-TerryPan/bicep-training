# Overview
This section is an introduction into Bicep logic and operators.  

Follow the sections below to complete `Part 2`

# Create a new branch
Tasks:
1. In your __local__ repository, create a new branch called `part-2`, based on `main`
1. Push this branch to your __remote__ repository

## Dependencies
- [Dependencies (DependsOn)](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/resource-dependencies)

### Implicit dependencies
An implicit dependency is created when one of the following conditions are met.
- One resource references another resource in the same deployment
- One resource is a nested resource of another
- One resource has a parent property

Tasks: 
1. Create a blob service in the storage account created in the last section. Please use the name 'default' for this resource and reference the storage account using it's symbolic name.

- [Blob Service](https://learn.microsoft.com/en-us/azure/templates/microsoft.storage/storageaccounts/blobservices?pivots=deployment-language-bicep)

### Explicit Dependencies
An explicit dependency is declared with the dependsOn property. The property accepts an array of resource identifiers, so you can specify more than one dependency.

For example:
```
dependsOn: [
  storageAccount
]
```

## Conditions

- [Conditions (if)](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/conditional-resource-deployment)

### Condition for deployment

Resources can be deployed conditionally by adding an if statement in the resource block.
```
resource storageAccount 'Microsoft.Storage/storageAccounts@2022-09-01' = if (deployStorage) {
  name: 'storageName
  location: location
}
```

### Conditional expression for properties

-[Conditional Expression (?:)](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/operators-logical#conditional-expression--)

Conditions can be used in resources to change a property based on a specified condition.

```
propertyName: condition ? <value if true> : <value if false>
```

Tasks: 
1. Create a parameter called `enablePublicNetworking`
1. Add conditions to change `publicNetworkAccess` to `'Disabled'` and `defaultAction` to `'Deny'` if the parameter is false.
```
publicNetworkAccess: 'Disabled'  
networkAcls: {
    bypass: 'AzureServices'
    defaultAction: 'Deny'
    ipRules: []
    virtualNetworkRules: []
}
```
*Above is the expected value without the condition function. Please add the condition operator.*

## Loops
- [Loops (for)](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/loops)

Loops are used to iterate over items in a collection. It can be used to create resources with many instances. Let's create a few blob containers in the storage account we created in the previous section.

Tasks: 
1. Create a variable with a list of strings containing blob container names
1. Create a resource using a for operator in the resource.
1. Deploy the blob containers.

Example:

```
resource storageAccount 'Microsoft.Storage/storageAccounts/blobServices/containers@2022-09-01' = [ for <item> in <collection>: {
  name: <item>
  parent: <blobServiceSymbolicName>
  properties: {}
}]
```

# Completion
You have made it to the end of `Part 2`, nice work! 

1. Create a pull request against your `main` branch to commit your branch changes.  
1. Take screenshots of the following in Azure and add to your pull request overview
    * the resource group you created
    * the deployment overview in Azure
1. Set your pull request to `auto-complete`. Select the following for post-completion  
    - Merge type: Merge (no fast forward)
    - Select: Delete `branch name` after merging
    - Leave other options unselected

Your mentor will review your work and reach out to you.

Once you have confirmation from your mentor, you can start `Part 3`. 