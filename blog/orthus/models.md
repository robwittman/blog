_---
title: Let's Create Models
---

Now that we've decided on some high level artifacts for our application, let's structure them into some 


### `Entity`
| Field | Type | Description | Defaults |
|---|---|---|---|
| `id` | UUID | Primary Key | | |
| `name` | `string` | | |

### `AwsCredentials`
| Field                   | Type       | Description               | Defaults |
|-------------------------|------------|---------------------------|---|
| `id`                    | UUID       | PrimaryKey                | | |
| `entity_id`             | `Entity.ID` |                           | |
| `identity`              | `string`    | The IAM Role or User name |          |
| `aws_access_key_id`     | `string`   | [Encrypted]               | |
| `aws_secret_access_key` | `string`   | [Encrypted]               | |
| `aws_iam_role_arn`      | `string`   |                           | |
| `aws_account_id`        | `string`   |                           | |

### `GoogleCredentials` 
| Field                          | Type       | Description | Defaults |
|--------------------------------|------------|-------------|---|
| `id`                           | UUID       | PrimaryKey  | | |
| `entity_id`                    | `Entity.ID` |             | |
| `google_service_account_email` | `string`    |             |          |
| `google_project_id`            | `string`   |             | |
| `google_service_account_key`   | `string`   | [Encrypted] | |
| `google_service_account`       | `string`   | | |

### `AzureCredentials` 
| Field | Type | Description | Defaults |
|---|---|---|---|
TODO: I don't like Azure

### DigitalOceanCredentials 
| Field | Type | Description | Defaults |
|---|---|---|---|
| `id` | UUID | PrimaryKey | |
| `digitalocean_access_token` | `string` | [Encrypted] | |

**Note**: Who knows if anyone wants to use DigitalOcean, but I have a soft spot for them
### Provider 
| Field | Type                    | Description | Defaults |
|---|-------------------------|---|---|
| `id` | UUID                    | Primary Key | |
| `name` | `strings`               | | |
| `credentials_id` | `${cloud}Credentials.ID` | | |
| `cloud` | `string` | | |

### Tenant 
| Field | Type | Description                  | Default |
|---|---|------------------------------|---|
| `id` | UUID | Primary Key                  | | | 
| `name` | `string` |                              | |
| `entity_id` | `Entity.ID` | Entity that owns this tenant | |
| `provider_id` | `Provider.ID` | ID of the provider configuration | |_
| `region` | `string` | Region for the provider | | |

### Admin 
- Inherited from Devise Models
### User
- Inherited from Devise Models


Alright, that should be enough for now. These resources let us
- Manage entities and  tenants
- Handle credential, provider, and tenant creation
- Configure user and admin login
- And verify we can connect to created accounts

Let's go ahead and get those created, and then we can jump into setting up our API 

