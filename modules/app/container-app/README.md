# Container Apps `[Microsoft.App/containerApps]`

This module deploys a Container App.

## Navigation

- [Resource Types](#Resource-Types)
- [Usage examples](#Usage-examples)
- [Parameters](#Parameters)
- [Outputs](#Outputs)
- [Cross-referenced modules](#Cross-referenced-modules)

## Resource Types

| Resource Type | API Version |
| :-- | :-- |
| `Microsoft.App/containerApps` | [2022-10-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.App/2022-10-01/containerApps) |
| `Microsoft.Authorization/locks` | [2020-05-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.Authorization/2020-05-01/locks) |
| `Microsoft.Authorization/roleAssignments` | [2022-04-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.Authorization/2022-04-01/roleAssignments) |

## Usage examples

The following section provides usage examples for the module, which were used to validate and deploy the module successfully. For a full reference, please review the module's test folder in its repository.

>**Note**: Each example lists all the required parameters first, followed by the rest - each in alphabetical order.

>**Note**: To reference the module, please use the following syntax `br:bicep/modules/app.container-app:1.0.0`.

- [Using large parameter set](#example-1-using-large-parameter-set)
- [Using only defaults](#example-2-using-only-defaults)

### Example 1: _Using large parameter set_

This instance deploys the module with most of its features enabled.


<details>

<summary>via Bicep module</summary>

```bicep
module containerApp 'br:bicep/modules/app.container-app:1.0.0' = {
  name: '${uniqueString(deployment().name, location)}-test-mcappcom'
  params: {
    // Required parameters
    containers: [
      {
        image: 'mcr.microsoft.com/azuredocs/containerapps-helloworld:latest'
        name: 'simple-hello-world-container'
        probes: [
          {
            httpGet: {
              httpHeaders: [
                {
                  name: 'Custom-Header'
                  value: 'Awesome'
                }
              ]
              path: '/health'
              port: 8080
            }
            initialDelaySeconds: 3
            periodSeconds: 3
            type: 'Liveness'
          }
        ]
        resources: {
          cpu: '<cpu>'
          memory: '0.5Gi'
        }
      }
    ]
    environmentId: '<environmentId>'
    name: 'mcappcom001'
    // Non-required parameters
    enableDefaultTelemetry: '<enableDefaultTelemetry>'
    location: '<location>'
    lock: {
      kind: 'CanNotDelete'
      name: 'myCustomLockName'
    }
    managedIdentities: {
      userAssignedResourcesIds: [
        '<managedIdentityResourceId>'
      ]
    }
    secrets: {
      secureList: [
        {
          name: 'customtest'
          value: '<value>'
        }
      ]
    }
    tags: {
      Env: 'test'
      'hidden-title': 'This is visible in the resource name'
    }
  }
}
```

</details>
<p>

<details>

<summary>via JSON Parameter file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "containers": {
      "value": [
        {
          "image": "mcr.microsoft.com/azuredocs/containerapps-helloworld:latest",
          "name": "simple-hello-world-container",
          "probes": [
            {
              "httpGet": {
                "httpHeaders": [
                  {
                    "name": "Custom-Header",
                    "value": "Awesome"
                  }
                ],
                "path": "/health",
                "port": 8080
              },
              "initialDelaySeconds": 3,
              "periodSeconds": 3,
              "type": "Liveness"
            }
          ],
          "resources": {
            "cpu": "<cpu>",
            "memory": "0.5Gi"
          }
        }
      ]
    },
    "environmentId": {
      "value": "<environmentId>"
    },
    "name": {
      "value": "mcappcom001"
    },
    // Non-required parameters
    "enableDefaultTelemetry": {
      "value": "<enableDefaultTelemetry>"
    },
    "location": {
      "value": "<location>"
    },
    "lock": {
      "value": {
        "kind": "CanNotDelete",
        "name": "myCustomLockName"
      }
    },
    "managedIdentities": {
      "value": {
        "userAssignedResourcesIds": [
          "<managedIdentityResourceId>"
        ]
      }
    },
    "secrets": {
      "value": {
        "secureList": [
          {
            "name": "customtest",
            "value": "<value>"
          }
        ]
      }
    },
    "tags": {
      "value": {
        "Env": "test",
        "hidden-title": "This is visible in the resource name"
      }
    }
  }
}
```

</details>
<p>

### Example 2: _Using only defaults_

This instance deploys the module with the minimum set of required parameters.


<details>

<summary>via Bicep module</summary>

```bicep
module containerApp 'br:bicep/modules/app.container-app:1.0.0' = {
  name: '${uniqueString(deployment().name, location)}-test-mcappmin'
  params: {
    // Required parameters
    containers: [
      {
        image: 'mcr.microsoft.com/azuredocs/containerapps-helloworld:latest'
        name: 'simple-hello-world-container'
        resources: {
          cpu: '<cpu>'
          memory: '0.5Gi'
        }
      }
    ]
    environmentId: '<environmentId>'
    name: 'mcappmin001'
    // Non-required parameters
    enableDefaultTelemetry: '<enableDefaultTelemetry>'
    location: '<location>'
    tags: {
      Env: 'test'
      'hidden-title': 'This is visible in the resource name'
    }
  }
}
```

</details>
<p>

<details>

<summary>via JSON Parameter file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "containers": {
      "value": [
        {
          "image": "mcr.microsoft.com/azuredocs/containerapps-helloworld:latest",
          "name": "simple-hello-world-container",
          "resources": {
            "cpu": "<cpu>",
            "memory": "0.5Gi"
          }
        }
      ]
    },
    "environmentId": {
      "value": "<environmentId>"
    },
    "name": {
      "value": "mcappmin001"
    },
    // Non-required parameters
    "enableDefaultTelemetry": {
      "value": "<enableDefaultTelemetry>"
    },
    "location": {
      "value": "<location>"
    },
    "tags": {
      "value": {
        "Env": "test",
        "hidden-title": "This is visible in the resource name"
      }
    }
  }
}
```

</details>
<p>


## Parameters

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`containers`](#parameter-containers) | array | List of container definitions for the Container App. |
| [`environmentId`](#parameter-environmentid) | string | Resource ID of environment. |
| [`name`](#parameter-name) | string | Name of the Container App. |

**Optional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`activeRevisionsMode`](#parameter-activerevisionsmode) | string | ActiveRevisionsMode controls how active revisions are handled for the Container app. |
| [`customDomains`](#parameter-customdomains) | array | Custom domain bindings for Container App hostnames. |
| [`dapr`](#parameter-dapr) | object | Dapr configuration for the Container App. |
| [`enableDefaultTelemetry`](#parameter-enabledefaulttelemetry) | bool | Enable telemetry via a Globally Unique Identifier (GUID). |
| [`exposedPort`](#parameter-exposedport) | int | Exposed Port in containers for TCP traffic from ingress. |
| [`ingressAllowInsecure`](#parameter-ingressallowinsecure) | bool | Bool indicating if HTTP connections to is allowed. If set to false HTTP connections are automatically redirected to HTTPS connections. |
| [`ingressExternal`](#parameter-ingressexternal) | bool | Bool indicating if app exposes an external http endpoint. |
| [`ingressTargetPort`](#parameter-ingresstargetport) | int | Target Port in containers for traffic from ingress. |
| [`ingressTransport`](#parameter-ingresstransport) | string | Ingress transport protocol. |
| [`initContainersTemplate`](#parameter-initcontainerstemplate) | array | List of specialized containers that run before app containers. |
| [`ipSecurityRestrictions`](#parameter-ipsecurityrestrictions) | array | Rules to restrict incoming IP address. |
| [`location`](#parameter-location) | string | Location for all Resources. |
| [`lock`](#parameter-lock) | object | The lock settings of the service. |
| [`managedIdentities`](#parameter-managedidentities) | object | The managed identity definition for this resource. |
| [`maxInactiveRevisions`](#parameter-maxinactiverevisions) | int | Max inactive revisions a Container App can have. |
| [`registries`](#parameter-registries) | array | Collection of private container registry credentials for containers used by the Container app. |
| [`revisionSuffix`](#parameter-revisionsuffix) | string | User friendly suffix that is appended to the revision name. |
| [`roleAssignments`](#parameter-roleassignments) | array | Array of role assignment objects that contain the 'roleDefinitionIdOrName' and 'principalId' to define RBAC role assignments on this resource. In the roleDefinitionIdOrName attribute. |
| [`scaleMaxReplicas`](#parameter-scalemaxreplicas) | int | Maximum number of container replicas. Defaults to 10 if not set. |
| [`scaleMinReplicas`](#parameter-scaleminreplicas) | int | Minimum number of container replicas. |
| [`scaleRules`](#parameter-scalerules) | array | Scaling rules. |
| [`secrets`](#parameter-secrets) | secureObject | The secrets of the Container App. |
| [`tags`](#parameter-tags) | object | Tags of the resource. |
| [`trafficLabel`](#parameter-trafficlabel) | string | Associates a traffic label with a revision. Label name should be consist of lower case alphanumeric characters or dashes. |
| [`trafficLatestRevision`](#parameter-trafficlatestrevision) | bool | Indicates that the traffic weight belongs to a latest stable revision. |
| [`trafficRevisionName`](#parameter-trafficrevisionname) | string | Name of a revision. |
| [`trafficWeight`](#parameter-trafficweight) | int | Traffic weight assigned to a revision. |
| [`volumes`](#parameter-volumes) | array | List of volume definitions for the Container App. |
| [`workloadProfileName`](#parameter-workloadprofilename) | string | Workload profile name to pin for container app execution. |

### Parameter: `activeRevisionsMode`

ActiveRevisionsMode controls how active revisions are handled for the Container app.
- Required: No
- Type: string
- Default: `'Single'`
- Allowed: `[Multiple, Single]`

### Parameter: `containers`

List of container definitions for the Container App.
- Required: Yes
- Type: array

### Parameter: `customDomains`

Custom domain bindings for Container App hostnames.
- Required: No
- Type: array
- Default: `[]`

### Parameter: `dapr`

Dapr configuration for the Container App.
- Required: No
- Type: object
- Default: `{object}`

### Parameter: `enableDefaultTelemetry`

Enable telemetry via a Globally Unique Identifier (GUID).
- Required: No
- Type: bool
- Default: `True`

### Parameter: `environmentId`

Resource ID of environment.
- Required: Yes
- Type: string

### Parameter: `exposedPort`

Exposed Port in containers for TCP traffic from ingress.
- Required: No
- Type: int
- Default: `0`

### Parameter: `ingressAllowInsecure`

Bool indicating if HTTP connections to is allowed. If set to false HTTP connections are automatically redirected to HTTPS connections.
- Required: No
- Type: bool
- Default: `True`

### Parameter: `ingressExternal`

Bool indicating if app exposes an external http endpoint.
- Required: No
- Type: bool
- Default: `True`

### Parameter: `ingressTargetPort`

Target Port in containers for traffic from ingress.
- Required: No
- Type: int
- Default: `80`

### Parameter: `ingressTransport`

Ingress transport protocol.
- Required: No
- Type: string
- Default: `'auto'`
- Allowed: `[auto, http, http2, tcp]`

### Parameter: `initContainersTemplate`

List of specialized containers that run before app containers.
- Required: No
- Type: array
- Default: `[]`

### Parameter: `ipSecurityRestrictions`

Rules to restrict incoming IP address.
- Required: No
- Type: array
- Default: `[]`

### Parameter: `location`

Location for all Resources.
- Required: No
- Type: string
- Default: `[resourceGroup().location]`

### Parameter: `lock`

The lock settings of the service.
- Required: No
- Type: object


| Name | Required | Type | Description |
| :-- | :-- | :--| :-- |
| [`kind`](#parameter-lockkind) | No | string | Optional. Specify the type of lock. |
| [`name`](#parameter-lockname) | No | string | Optional. Specify the name of lock. |

### Parameter: `lock.kind`

Optional. Specify the type of lock.

- Required: No
- Type: string
- Allowed: `[CanNotDelete, None, ReadOnly]`

### Parameter: `lock.name`

Optional. Specify the name of lock.

- Required: No
- Type: string

### Parameter: `managedIdentities`

The managed identity definition for this resource.
- Required: No
- Type: object


| Name | Required | Type | Description |
| :-- | :-- | :--| :-- |
| [`systemAssigned`](#parameter-managedidentitiessystemassigned) | No | bool | Optional. Enables system assigned managed identity on the resource. |
| [`userAssignedResourcesIds`](#parameter-managedidentitiesuserassignedresourcesids) | No | array | Optional. The resource ID(s) to assign to the resource. |

### Parameter: `managedIdentities.systemAssigned`

Optional. Enables system assigned managed identity on the resource.

- Required: No
- Type: bool

### Parameter: `managedIdentities.userAssignedResourcesIds`

Optional. The resource ID(s) to assign to the resource.

- Required: No
- Type: array

### Parameter: `maxInactiveRevisions`

Max inactive revisions a Container App can have.
- Required: No
- Type: int
- Default: `0`

### Parameter: `name`

Name of the Container App.
- Required: Yes
- Type: string

### Parameter: `registries`

Collection of private container registry credentials for containers used by the Container app.
- Required: No
- Type: array
- Default: `[]`

### Parameter: `revisionSuffix`

User friendly suffix that is appended to the revision name.
- Required: No
- Type: string
- Default: `''`

### Parameter: `roleAssignments`

Array of role assignment objects that contain the 'roleDefinitionIdOrName' and 'principalId' to define RBAC role assignments on this resource. In the roleDefinitionIdOrName attribute.
- Required: No
- Type: array


| Name | Required | Type | Description |
| :-- | :-- | :--| :-- |
| [`condition`](#parameter-roleassignmentscondition) | No | string | Optional. The conditions on the role assignment. This limits the resources it can be assigned to. e.g.: @Resource[Microsoft.Storage/storageAccounts/blobServices/containers:ContainerName] StringEqualsIgnoreCase "foo_storage_container" |
| [`conditionVersion`](#parameter-roleassignmentsconditionversion) | No | string | Optional. Version of the condition. |
| [`delegatedManagedIdentityResourceId`](#parameter-roleassignmentsdelegatedmanagedidentityresourceid) | No | string | Optional. The Resource Id of the delegated managed identity resource. |
| [`description`](#parameter-roleassignmentsdescription) | No | string | Optional. The description of the role assignment. |
| [`principalId`](#parameter-roleassignmentsprincipalid) | Yes | string | Required. The principal ID of the principal (user/group/identity) to assign the role to. |
| [`principalType`](#parameter-roleassignmentsprincipaltype) | No | string | Optional. The principal type of the assigned principal ID. |
| [`roleDefinitionIdOrName`](#parameter-roleassignmentsroledefinitionidorname) | Yes | string | Required. The name of the role to assign. If it cannot be found you can specify the role definition ID instead. |

### Parameter: `roleAssignments.condition`

Optional. The conditions on the role assignment. This limits the resources it can be assigned to. e.g.: @Resource[Microsoft.Storage/storageAccounts/blobServices/containers:ContainerName] StringEqualsIgnoreCase "foo_storage_container"

- Required: No
- Type: string

### Parameter: `roleAssignments.conditionVersion`

Optional. Version of the condition.

- Required: No
- Type: string
- Allowed: `[2.0]`

### Parameter: `roleAssignments.delegatedManagedIdentityResourceId`

Optional. The Resource Id of the delegated managed identity resource.

- Required: No
- Type: string

### Parameter: `roleAssignments.description`

Optional. The description of the role assignment.

- Required: No
- Type: string

### Parameter: `roleAssignments.principalId`

Required. The principal ID of the principal (user/group/identity) to assign the role to.

- Required: Yes
- Type: string

### Parameter: `roleAssignments.principalType`

Optional. The principal type of the assigned principal ID.

- Required: No
- Type: string
- Allowed: `[Device, ForeignGroup, Group, ServicePrincipal, User]`

### Parameter: `roleAssignments.roleDefinitionIdOrName`

Required. The name of the role to assign. If it cannot be found you can specify the role definition ID instead.

- Required: Yes
- Type: string

### Parameter: `scaleMaxReplicas`

Maximum number of container replicas. Defaults to 10 if not set.
- Required: No
- Type: int
- Default: `1`

### Parameter: `scaleMinReplicas`

Minimum number of container replicas.
- Required: No
- Type: int
- Default: `0`

### Parameter: `scaleRules`

Scaling rules.
- Required: No
- Type: array
- Default: `[]`

### Parameter: `secrets`

The secrets of the Container App.
- Required: No
- Type: secureObject
- Default: `{object}`

### Parameter: `tags`

Tags of the resource.
- Required: No
- Type: object
- Default: `{object}`

### Parameter: `trafficLabel`

Associates a traffic label with a revision. Label name should be consist of lower case alphanumeric characters or dashes.
- Required: No
- Type: string
- Default: `'label-1'`

### Parameter: `trafficLatestRevision`

Indicates that the traffic weight belongs to a latest stable revision.
- Required: No
- Type: bool
- Default: `True`

### Parameter: `trafficRevisionName`

Name of a revision.
- Required: No
- Type: string
- Default: `''`

### Parameter: `trafficWeight`

Traffic weight assigned to a revision.
- Required: No
- Type: int
- Default: `100`

### Parameter: `volumes`

List of volume definitions for the Container App.
- Required: No
- Type: array
- Default: `[]`

### Parameter: `workloadProfileName`

Workload profile name to pin for container app execution.
- Required: No
- Type: string
- Default: `''`


## Outputs

| Output | Type | Description |
| :-- | :-- | :-- |
| `location` | string | The location the resource was deployed into. |
| `name` | string | The name of the Container App. |
| `resourceGroupName` | string | The name of the resource group the Container App was deployed into. |
| `resourceId` | string | The resource ID of the Container App. |
| `systemAssignedMIPrincipalId` | string | The principal ID of the system assigned identity. |

## Cross-referenced modules

_None_
