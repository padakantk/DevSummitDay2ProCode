<p align="center">
  <img src="/Images/FedDevSummitBanner.jpg?raw=true" />
</p>

# Microsoft Federal Developer Summit – Day 2 Pro Code Track

# Overview
This repo is for the second day pro code track for Microsoft Federal Developer Summit on November 13th-14th, 20204.  It contains a Python Streamlit bot which leverages Azure OpenAI and AI Search.

<p align="center">
  <img src="/Images/icecreambotss.png?raw=true" />
</p>

## Prerequisites
**Github Codespaces** or
1. Bicep v0.30.3 or higher
2. Az CLI (moderately current version)
3. Contributor and User Access Administrator on a subscription (Or Owner)
4. VSCode w/ necessary extensions, or ability to add them

# Getting Started

1. Create a new fork of this repo in your personal GitHub account
2. In newly created repo(in your account) launch a new Codespaces workspace
3. Run `az login` - use Dev Summit provided login and password
4. *Optional* Run `az account set -s <subscriptionId>` if more than one subscription is present
5. Run `cd infra` to navigate to the directory containing the bicep deployment code
6. Run `az deployment sub create --template-file main.bicep --parameters main.parameters.json --location eastus2 --name "icecream-chat-*YOUR INITALS*"`

  *note*: The `--name` parameter is a global variable used to set both the name of the deployment at the subscription level as well as the resources that are being provisioned.

  *note*: Azure OpenAI, AI Search, and Multi-service account deploy within East US. To update this value change `param locationAI string = 'eastus'` within `resources.bicep` on line #27 or specify it as an additional parameter with `locationAI="<desiredRegion>"`


After deployment is complete, which will take approximately 30-35 minutes (API Management is the long running process, the environment can start being used before that time but do not close the terminal session), copy the following outputs to a safe place for later use:
`app_url`, `appServcePrincipalKey`, `appServicePrincipalId`, `azure_subscription_id`, `azure_subscripton_name`, and `azure_tenant_Id`
```json
"outputs": {
      "app_url": {
        "type": "String",
        "value": "https://<your-site>.azurewebsites.net"
      },
      "appServicePrincipalId": {
        "type": "String",
        "value": "00000000-0000-0000-0000-000000000000"
      },
      "appServicePrincipalKey": {
        "type": "String",
        "value": "<your-super!secret_.key>"
      },
      "azure_subscription_id": {
        "type": "String",
        "value": "00000000-0000-0000-0000-000000000000"
      },
      "azure_subscription_name": {
        "type": "String",
        "value": "<friendly-subscription-name>"
      },
      "azure_tenant_id": {
        "type": "String",
        "value": "00000000-0000-0000-0000-000000000000"
      }
    },
```

<!-- <img src="/Images/azdoutput.png?raw=true" /> -->
### Session Steps
1. Follow steps for fork repo and deploy environment
2. Review RBAC and make updates to necessary services
3. Review storage, upload icecream files to be indexed
4. Deploy Azure OpenAI models - gpt-4o, text-ada-embedding
5. Create vector index from AI search
6. Use github actions to push image
7. Update App Service, create/sen environment variables
8. Use OpenAI Playground to perform prompt engineering, update code with refined prompt
9. Implement APIM


for creating a container using :az acr build --image dev-summit/ice-cream-bot:2024114-297979 --registry icecreamchatsolutionkpp2979acrybhxicthv6rca --file Dockerfile .