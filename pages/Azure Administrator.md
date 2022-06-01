- Tools used in Azure to 'admin' MS Azure resources are AZ Portal, AZ Cloud Shell, AZ Powershell, AZ CLI
- AZ Cloud Shell is an interactive, browser accessible shell for managing AZ resources.
  collapsed:: true
	- Authenticates automatically for instant access
	- Times out after 20 mins of inactivity
	- Persists $HOME using 5 GB image held in your fileshare.
	- Permissions are set as regular Linux user in Bash
- Azure PowerShell is a module you add to Windows PowerShell or PowerShell core.
  collapsed:: true
	- Az is formal name for Azure PowerShell module that contains cmdlets to work with Azure features. Available on https://github.com/Azure/azure-powershell
- Azure CLI - a command-line program to connect to Azure and execute Administrative commands on Azure resources. It runs on Linux, macOS, Windows.
  collapsed:: true
	- Can use --help here like linux. E.g. `az storage blob --help`
-
- ^^Azure Resource Manager^^
  collapsed:: true
	- ARM or Azure Resource Manager enables you to work with resources in your solution as a group. You can deploy, update or delete all resources of your solution in a single, coordinated operation. You can use tagging, security, auditing features to help you manage your resources after deployment.
	- Consistent Management Layer.
		- All tools - Azure PowerShell, CLI, Cloudshell etc. interact with ARM API to manage all resources.
		- You can monitor resources in a group instead having to do it individually.
	- **resource** - A manageable item in Azure. VM, Storage account, webapp, database, virtual network.
	- **resource group** - A container that holds related resources together in AZ solution.
	- **resource provider** - A services that supplies resources you can deploy and manager via Resource Manager. E.g. Microsoft.Compute supplies VMs, Microsoft.Storage supplies storage account resource, Micrsoft.Web supplies resources related to web apps
	- **template** - A JavaScript Object Notation (JSON) file that defines one or more resources to deploy.
	- **declarative syntax**
- ^^Resource Groups^^
  collapsed:: true
	- resources can only exist in **one** resource group.
	- Resource group cannot be renamed
	- can have different services
	- can have resources from many different regions.
	- **Azure Resource Manager Locks**
	  collapsed:: true
		- Concern with ease at which resource groups can be deleted.
		- Resource manager locks allows orgs to put a structure in place that prevents accidental deletion of resources in Azure.
		- You can associate a lock with a subs, resource group or resource
		- Locks are inherited by child resources.
		- Lock types -
			- 2. Delete locks , prevents deletion.
			- 1. Read only locks - prevents changes to resources
	- **Reorganize Azure Resources**
	  collapsed:: true
		-
		- Can move resource either to new subscription or new resource group in same subs.
		- While moving both source and target groups are locked during operation. Write and delete operations are blocked until move completes.
	- **Remove resources and resource groups**
	  collapsed:: true
		- Deleting resource group deletes all resources contained within it. That resource group might contain
		- PowerShell - `Remove-AzResourceGroup -Name "ContosoRG01"`
		-
	- **Determine resource Limits** 
	  collapsed:: true
		- Limits shown are limits for your subscription.
		- All resources have a maximum limit listed in Azure limits
- ^^Azure Resource Manager Templates^^
  collapsed:: true
	- An Azure Resource manager Template precisely defines all resource manager resources in a deployment. You can deploy a Resource Manager Template into a resource group as a single operation.
	- Make deployments faster and repeatable.
	- Template benefits
		- improves consistency
		- complex deployments
		- Templates are codes.
		- Promote reuse - staging -> production
		- linkable
		- orchestration
	- Schema of a Template
		- written in JSON format, allows to express data stored as an object in text. JSON document is a key-value pair document. Each key is a string and its value can be a string, a number, a boolean expression, list of values, an object (other key-value pairs)
		- Example of Az Resource Manager Template parameters
		  ````
		  "parameters": {
		      "<parameter-name>" : {
		          "type" : "<type-of-parameter-value>",
		          "defaultValue": "<default-value-of-parameter>",
		          "allowedValues": [ "<array-of-allowed-values>" ],
		          "minValue": <minimum-value-for-int>,
		          "maxValue": <maximum-value-for-int>,
		          "minLength": <minimum-length-for-string-or-array>,
		          "maxLength": <maximum-length-for-string-or-array-parameters>,
		          "metadata": {
		          "description": "<description-of-the parameter>"
		          }
		      }
		  }
		  ````
		- example for VMs username and password
		  ````
		  "parameters": {
		    "adminUsername": {
		      "type": "string",
		      "metadata": {
		        "description": "Username for the Virtual Machine."
		      }
		    },
		    "adminPassword": {
		      "type": "securestring",
		      "metadata": {
		        "description": "Password for the Virtual Machine."
		      }
		    }
		  }
		  ````
	- **Azure Bicep**
		- Azure Bicep is a domain-specific language (DSL) using declarive syntax to deply Az resources.
		- Bicep has simpler syntax, modules to break complexity and bring resuablitiy, automatic dependency management,
-