Sample piepeline yaml file

```yaml
# Starter pipeline
# Start with a minimal pipeline that you can customize to build and deploy your code.
# Add steps that build, run tests, deploy, and more:

# https://aka.ms/yaml

trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- script: echo Hello, world!
  displayName: 'Run a one-line script'

- task: AzureResourceManagerTemplateDeployment@3
  inputs:
    deploymentScope: 'Resource Group'
    azureResourceManagerConnection: 'Visual Studio Enterprise Subscription(74a78629-ac6d-55db-a77a-abcabcacbaac)'
    subscriptionId: '74a78629-ac6d-55db-a77a-abcabcacbaac'
    action: 'Create Or Update Resource Group'
    resourceGroupName: 'GJS-MS150-MDFC2'
    location: 'East Asia'
    templateLocation: 'Linked artifact'
    csmFile: 'main.bicep'
    deploymentMode: 'Incremental'

- task: AzureResourceManagerTemplateDeployment@3
  inputs:
    deploymentScope: 'Resource Group'
    azureResourceManagerConnection: 'Visual Studio Enterprise Subscription(74a78629-ac6d-55db-a77a-abcabcacbaac)'
    subscriptionId: '74a78629-ac6d-55db-a77a-abcabcacbaac'
    action: 'Create Or Update Resource Group'
    resourceGroupName: 'gjs-sentinel'
    location: 'East Asia'
    templateLocation: 'Linked artifact'
    csmFile: 'testrule.bicep'
    overrideParameters: '-workspaceName gjs-sentinel-workspace1'
    deploymentMode: 'Incremental'


- task: AzureResourceManagerTemplateDeployment@3
  inputs:
    deploymentScope: 'Resource Group'
    azureResourceManagerConnection: 'Visual Studio Enterprise Subscription(74a78629-ac6d-55db-a77a-abcabcacbaac)'
    subscriptionId: '74a78629-ac6d-55db-a77a-abcabcacbaac'
    action: 'Create Or Update Resource Group'
    resourceGroupName: 'gjs-sentinel'
    location: 'East Asia'
    templateLocation: 'Linked artifact'
    csmFile: 'gjs-test0221.bicep'
    overrideParameters: '-workspaceName gjs-sentinel-workspace1'
    deploymentMode: 'Incremental'    
    
 ```
