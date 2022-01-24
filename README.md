** Disclaimer
For more info of this project see https://github.com/Azure-Samples/jmeter-aci-terraform

** Steps:
- Import into an Azure Repository
- Create a Library and maintain at least following variables
  - AZURE_SERVICE_CONNECTION_NAME = name of the service connection
  - AZURE_SUBSCRIPTION_ID = id of subscription used
  - TF_VAR_JMETER_ACR_NAME = name of the container registry
  - TF_VAR_JMETER_ACR_RESOURCE_GROUP_NAME = same as TF_VAR_RESOURCE_GROUP_NAME
  - TF_VAR_JMETER_DOCKER_IMAGE = justb4/jmeter:5.1.1
  - TF_VAR_JMETER_JMX_FILE = sample.jmx
  - TF_VAR_JMETER_WORKERS_COUNT = 4
  - TF_VAR_PREFIX = jmeter
  - TF_VAR_RESOURCE_GROUP_NAME = name of the existing resource group to be used
  - TF_VAR_USERS_PER_NODE = 1
- Create the Azure pipeline based on the yml file
  - It will import an existing resource group as this is required by dev ops

** Error:
Pipeline break does not always happen, but on average 33 % of the time for 4 workers, higher failure chance when more workers are needed
```
| Error: creating/updating Container Group: (Name "jmeter-worker3" / Resource Group "####"): containerinstance.ContainerGroupsClient#CreateOrUpdate: Failure sending request: StatusCode=409 -- Original Error: Code="ServiceAssociationLinkNotReady" Message="Network is not ready for container group 'jmeter-worker3'. Please try again."
|
| with azurerm_container_group.jmeter_workers[3],
| on main.tf line 75, in resource "azurerm_container_group" "jmeter_workers":
| 75: resource "azurerm_container_group" "jmeter_workers" {
|
|
##[error]Bash exited with code '1'.
```

** Issues:
- https://github.com/Azure-Samples/jmeter-aci-terraform/issues/81
- https://github.com/hashicorp/terraform-provider-azurerm/issues/15025