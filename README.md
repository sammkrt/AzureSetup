# AzureSetup

## Using Azure

```
brew install azure-cli
```

## Azure CLI

```
az login
```
<ol>
  <li>Create a deployment user</li>
  <li>Create a resource group
        1. logical container for all things about the app</li>
  <li>Create the web application
        1. a logical representation of our app in Azure</li>
  <li>Push code from our git to Azure
        1. Just using git</li>
</ol>

## MOVING AN APP TO AZURE - CLI

```
az login
git clone https://github.com/Azure-Samples/dotnet-core-api
cd dotnet-core-api
dotnet restore
dotnet run
```

## CREATE A DEPLOYMENT USER
```
az webapp deployment user set --user-name <username> --password <password>
```

## CLI: CREATE A RESOURCE-GROUP

<h4> List free locations</h4>

```
az appservice list-locations --sku FREE
  ```

<h4> Create resource here in Western Europe</h4>

```
az group create --name firstAppResourceGroup --location "West Europe"
  ```

<h4> Create an AppService plan</h4>

```
az appservice plan create --name firstAppServicePlan --resource-group firstAppResourceGroup --sku FREE
  ```

## CREATE THE WEB APP

```
az webapp create --resource-group firstAppResourceGroup --plan firstAppServicePlan --name firstAppCli --deployment-local-git
  ```

## NOW WE PUSH OUR APP


```
az webapp config appsettings set --name firstAppCli --resource-group firstAppResourceGroup --settings DEPLOYMENT_BRANCH='main'
  ```

<h4> Add Azure remote</h4>

```
git remote add azure <deploymentLocalGitUrl-from-create-ste
   ```

<h4> Push, using the deployment user</h4>

```
git push azure main
```

## REMOVE THE APP

```
az group delete --name firstAppResourceGroup
  ```



