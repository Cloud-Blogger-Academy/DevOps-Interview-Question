# Real Time Terraform Interview Questions & Answers

**Cracking your next DevOps/Cloud interview? These are practical Terraform questions recruiters commonly ask — with clear, interview-ready answers and commands/code where useful.**

> 💡 Want to build real Terraform + Azure projects? Explore the Cloud Blogger Academy Terraform training.

---

### 1. What is Terraform?

Terraform is an Infrastructure as Code (IaC) tool from HashiCorp. It lets you define infrastructure such as Azure VMs, VNets, AKS, Storage Accounts, and databases as code and provision them consistently.

```hcl
resource "azurerm_resource_group" "example" {
  name     = "rg-demo"
  location = "East US"
}
```

**Interview tip:** Terraform is declarative — you describe the desired state and Terraform determines the actions required to reach it.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 2. Why do you use Terraform for infrastructure provisioning instead of other IaC tools?

Terraform is useful because it is declarative, supports many cloud providers, uses reusable modules, maintains state, provides execution plans, and integrates well with CI/CD.

```bash
terraform plan
terraform apply
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 3. What is Infrastructure as Code (IaC)?

IaC means managing infrastructure through machine-readable configuration files instead of manually creating resources through a portal.

```hcl
resource "azurerm_storage_account" "example" {
  name                     = "stexample123"
  resource_group_name      = "rg-demo"
  location                 = "East US"
  account_tier             = "Standard"
  account_replication_type = "LRS"
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 4. What is Terraform architecture?

Terraform generally works through configuration, providers, state, and the Terraform engine. Terraform reads the configuration, refreshes/uses state, builds a dependency graph, creates a plan, and calls the provider APIs to make changes.

```text
Terraform Configuration
        |
        v
Terraform Core
        |
        +---- State
        |
        +---- Provider
                |
                v
             Azure API
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 5. Explain the Terraform workflow.

The common workflow is:

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
terraform destroy
```

`init` initializes the working directory, `plan` previews changes, and `apply` executes them.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 6. What is a Terraform Provider?

A provider is a plugin that allows Terraform to communicate with an API platform such as Azure, AWS, or GitHub.

```hcl
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 4.0"
    }
  }
}

provider "azurerm" {
  features {}
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 7. What is the difference between the terraform block and provider block?

The `terraform` block defines Terraform/provider requirements and backend configuration. The `provider` block configures how Terraform connects to a provider.

```hcl
terraform {
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
    }
  }
}

provider "azurerm" {
  features {}
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 8. What is Terraform HCL?

HCL (HashiCorp Configuration Language) is the configuration language commonly used to write Terraform files.

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-demo"
  location = "East US"
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 9. What is a Terraform resource?

A resource represents infrastructure that Terraform creates and manages.

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-demo"
  location = "East US"
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 10. What are Terraform attributes?

Attributes are values/configuration arguments associated with resources or other blocks.

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-demo"       # attribute
  location = "East US"       # attribute
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 11. What are Terraform functions?

Terraform functions perform operations on values, such as string manipulation, collection processing, and conversions.

```hcl
locals {
  environment_name = upper("dev")
  vm_count         = length(["vm1", "vm2"])
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 12. What is terraform fmt?

`terraform fmt` formats Terraform configuration into the standard style.

```bash
terraform fmt -recursive
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 13. What is a Terraform linter?

A linter checks Terraform code for style, configuration, and potential problems. Common tools include TFLint, tfsec, and Checkov.

```bash
terraform fmt -check
terraform validate
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 14. What is the -parallelism flag?

`-parallelism` controls how many independent Terraform operations can execute concurrently.

```bash
terraform apply -parallelism=20
```

Use it carefully because increasing concurrency can increase API throttling.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 15. What logging levels are supported by Terraform?

Terraform supports logging through the `TF_LOG` environment variable. Common levels include `TRACE`, `DEBUG`, `INFO`, `WARN`, and `ERROR`.

```bash
export TF_LOG=DEBUG
terraform plan
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 16. What is the process to install and set up Terraform?

Install Terraform, verify the binary, configure cloud authentication, create a `.tf` configuration, and initialize the working directory.

```bash
terraform version
terraform init
terraform validate
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 17. What setup is required before Terraform runs in a CI/CD pipeline?

Typically you need Terraform installed on the runner, provider credentials, backend configuration, repository access, required variables, and security validation.

```text
Git -> Validate -> Security Scan -> Plan -> Approval -> Apply
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 18. What happens during terraform init?

Terraform initializes the working directory, downloads required providers/modules, and configures the backend.

```bash
terraform init
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 19. Where do you run terraform init and terraform apply in CI/CD?

They are normally executed as pipeline stages.

```yaml
stages:
  - validate
  - plan
  - apply
```

```bash
terraform init
terraform plan
terraform apply -auto-approve
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 20. What are the different Terraform variable types?

Common types are `string`, `number`, `bool`, `list`, `set`, `map`, `tuple`, and `object`.

```hcl
variable "location" {
  type    = string
  default = "East US"
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 21. Explain Terraform data types.

Terraform supports primitive types such as string, number and bool, plus collection/structural types such as list, set, map, tuple and object.

```hcl
variable "vm_names" {
  type = list(string)
}

variable "tags" {
  type = map(string)
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 22. What are Type Constraints?

Type constraints specify what type of value a variable accepts.

```hcl
variable "vm_size" {
  type = string
}
```

They improve validation and make modules predictable.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 23. Difference between variable.tf and terraform.tfvars?

`variables.tf` usually declares variables. `terraform.tfvars` supplies values for those variables.

```hcl
# variables.tf
variable "location" {
  type = string
}
```

```hcl
# terraform.tfvars
location = "East US"
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 24. How do you define a default variable value?

```hcl
variable "environment" {
  type    = string
  default = "dev"
}
```

If no value is supplied, Terraform uses the default.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 25. Difference between variables, locals and outputs?

Variables are inputs, locals are reusable calculated values inside a module, and outputs expose values from a module.

```hcl
variable "location" {
  type = string
}

locals {
  environment = "dev"
}

output "resource_group_id" {
  value = azurerm_resource_group.rg.id
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 26. How do you pass variables from root to child module?

```hcl
module "network" {
  source   = "./modules/network"
  location = var.location
  vnet_cidr = var.vnet_cidr
}
```

The child module declares the corresponding variables.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 27. How do you mark a variable sensitive?

```hcl
variable "admin_password" {
  type      = string
  sensitive = true
}
```

This prevents the value from being displayed normally in CLI output.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 28. If a variable is sensitive, how can you see it in tfstate?

`Sensitive` does not mean the value is encrypted inside state. If the value is stored in state, it may still exist there. Protect the state with a secure remote backend and strict access controls.

```bash
terraform state pull
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 29. What is a Terraform module?

A module is a reusable collection of Terraform configuration files.

```text
modules/
└── network/
    ├── main.tf
    ├── variables.tf
    └── outputs.tf
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 30. Difference between Root Module and Child Module?

The root module is the directory where Terraform is executed. A child module is called by another module.

```hcl
module "network" {
  source = "./modules/network"
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 31. Explain the folder structure of a Terraform module.

A common structure is:

```text
terraform/
├── main.tf
├── variables.tf
├── outputs.tf
├── providers.tf
├── terraform.tfvars
└── modules/
    └── network/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 32. How do you follow a parent-child module approach?

The root module supplies inputs to child modules, and child modules return outputs.

```hcl
module "network" {
  source = "./modules/network"
}

module "vm" {
  source     = "./modules/vm"
  subnet_id  = module.network.subnet_id
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 33. Difference between Resource Module and Pattern Module?

A resource module focuses on a reusable infrastructure component. A pattern module combines multiple resources into a reusable architecture pattern.

```text
Resource Module: Storage Account
Pattern Module:  VNet + Subnets + NSGs + Private Endpoint
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 34. What is a Pattern Module?

A Pattern Module represents a repeatable architecture pattern rather than a single resource.

```text
Application Pattern
├── Resource Group
├── VNet
├── Subnet
├── NSG
└── Private Endpoint
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 35. How do modules communicate?

Modules communicate primarily through input variables and output values.

```hcl
module "vm" {
  source    = "./modules/vm"
  subnet_id = module.network.subnet_id
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 36. How do you pass VNet values to a VM module?

Expose the required value as an output from the network module and pass it into the VM module.

```hcl
subnet_id = module.network.subnet_id
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 37. Why can't a child module directly access root variables?

Terraform modules have their own scope. Values must be explicitly passed through module inputs.

```hcl
module "vm" {
  source   = "./modules/vm"
  location = var.location
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 38. How do you design reusable enterprise Terraform modules?

I keep modules focused, parameterized, version-controlled, documented, secure, and environment-independent.

```text
Root Module
   |
   +-- Network Module
   +-- Security Module
   +-- Compute Module
   +-- Monitoring Module
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 39. How do you structure modules using DRY?

Put common infrastructure into reusable modules and pass environment-specific values through variables/tfvars.

```hcl
module "vm" {
  source   = "./modules/vm"
  for_each = var.vms
  name     = each.key
  size     = each.value.size
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 40. How can one module be reused across Dev, UAT and Prod?

Keep the module generic and supply different variable values per environment.

```text
env/
├── dev/
├── uat/
└── prod/

modules/
└── vm/
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 41. Have you created custom Terraform modules?

A good interview answer is: "Yes. I create reusable modules for common infrastructure such as resource groups, networking, VMs, Key Vault, Storage, and AKS, with variables and outputs so the same module can be reused across environments."

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 42. How would you design a reusable AKS module?

I would expose variables for cluster name, location, Kubernetes version, node pools, networking, identity, RBAC, autoscaling and tags, while keeping the implementation inside the child module.

```hcl
module "aks" {
  source       = "./modules/aks"
  cluster_name = var.cluster_name
  location     = var.location
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 43. What variables and outputs are common in an AKS module?

Typical inputs include cluster name, location, Kubernetes version, node pools, networking and identity. Outputs can include cluster ID, kubelet identity and cluster name.

```hcl
output "cluster_id" {
  value = azurerm_kubernetes_cluster.aks.id
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 44. Have you worked with Azure Verified Modules or CAF modules?

A strong answer is: "Yes, I evaluate Azure Verified Modules/CAF modules where they provide a standardized implementation. I also build custom modules when project-specific requirements need more control."

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 45. Explain your Terraform production folder structure.

```text
terraform/
├── environments/
│   ├── dev/
│   ├── uat/
│   └── prod/
├── modules/
│   ├── network/
│   ├── vm/
│   ├── aks/
│   └── keyvault/
└── README.md
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 46. How do you structure root modules, child modules, locals, for_each and tfvars?

Root modules compose the infrastructure, child modules implement reusable components, locals simplify expressions, `for_each` handles repeated objects, and tfvars provide environment values.

```hcl
module "vm" {
  source   = "./modules/vm"
  for_each = var.vms
  name     = each.key
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 47. How do you structure Terraform for Dev, QA, Stage and Production?

I separate environment-specific configuration/state while reusing common modules.

```text
environments/
├── dev/
├── qa/
├── stage/
└── prod/
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 48. How do you manage Terraform across multiple environments?

Use reusable modules, environment-specific variables, separate state, controlled CI/CD pipelines, and approvals for production.

```text
Module -> Dev
       -> QA
       -> Stage
       -> Prod
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 49. How do you standardize Terraform across 20+ cloud accounts?

I use version-controlled modules, provider aliases, centralized policies, CI/CD templates, security scans, remote state, version pinning and code review.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 50. How do you structure Terraform for multiple Azure subscriptions?

Use provider aliases and pass the appropriate provider into modules.

```hcl
provider "azurerm" {
  alias           = "prod"
  subscription_id = var.prod_subscription_id
  features {}
}

module "prod" {
  source    = "./modules/network"
  providers = { azurerm = azurerm.prod }
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 51. What is a Terraform State File?

The state file records Terraform's knowledge of managed resources and their relationships to the configuration.

```text
terraform.tfstate
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 52. Why is Terraform State required?

Terraform uses state to map configuration to real infrastructure and determine what needs to be created, changed or destroyed.

```bash
terraform plan
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 53. When is the State File created?

Terraform creates/updates state as it manages resources, typically during operations such as `terraform apply`.

```bash
terraform apply
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 54. Where is the State File stored?

It can be stored locally or remotely. In production, remote state is normally preferred.

```text
Local:  terraform.tfstate
Remote: Azure Blob / Terraform Cloud / Enterprise
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 55. How do you manage Terraform State in an enterprise?

Use a remote backend, state locking, encryption, RBAC, versioning, restricted access, backups and separate state per environment/workload.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 56. What is Remote State?

Remote state means Terraform state is stored in a shared backend instead of only on a developer's local machine.

```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "rg-tfstate"
    storage_account_name = "sttfstate"
    container_name       = "tfstate"
    key                  = "prod.tfstate"
  }
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 57. Why store State remotely?

Remote state provides centralized access, collaboration, locking, backup/versioning capabilities and better security controls.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 58. What is a Terraform Backend?

A backend defines where Terraform stores state and, depending on the backend, how state locking/remote operations are handled.

```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "rg-tfstate"
    storage_account_name = "sttfstate"
    container_name       = "tfstate"
    key                  = "prod.tfstate"
  }
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 59. How do you configure Azure Blob Storage as a backend?

Create a secure Storage Account/container and configure the `azurerm` backend.

```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "rg-tfstate"
    storage_account_name = "sttfstate"
    container_name       = "tfstate"
    key                  = "prod.tfstate"
  }
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 60. How do you migrate local state to remote state?

Configure the remote backend and run:

```bash
terraform init -migrate-state
```

Terraform asks for confirmation and migrates the existing state.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 61. How do you manage remote state for multiple subscriptions?

Use separate state keys/backends or logically isolated state configurations, and authenticate against the correct subscription.

```text
prod-subscription -> prod.tfstate
dev-subscription  -> dev.tfstate
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 62. How do you encrypt and secure Terraform State?

Use a secure remote backend with encryption at rest, TLS in transit, RBAC/least privilege, private networking where appropriate, state locking, auditing and restricted access.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 63. What is Terraform State Locking?

State locking prevents multiple Terraform operations from modifying the same state at the same time.

```text
Engineer A -> LOCK -> Apply
Engineer B -> WAIT
Engineer A -> UNLOCK
Engineer B -> Apply
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 64. How does State Locking work?

When Terraform starts a state-changing operation, the backend obtains a lock. Other operations against that same state should wait or fail until the lock is released.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 65. What happens if two engineers run terraform apply simultaneously?

With a locking-capable backend, one operation obtains the lock and the other cannot modify the same state simultaneously.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 66. What happens when two developers update the same state simultaneously?

State locking protects against concurrent state modifications. Teams should still use CI/CD and controlled ownership to avoid conflicting infrastructure changes.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 67. When would you use terraform force-unlock?

Only when a lock is genuinely stale and the original operation is no longer running.

```bash
terraform force-unlock LOCK_ID
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 68. What precautions should you take before force-unlock?

Verify that no Terraform process is still running and confirm the lock belongs to a failed/stale operation. Incorrectly removing a valid lock can cause concurrent state changes.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 69. How do you resolve a locked state in Terraform Enterprise without local Terraform?

Use the Terraform Enterprise UI/API/workspace controls to investigate the run/lock and resolve the stale lock according to the platform's supported procedure.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 70. How is Terraform State managed in Terraform Enterprise?

Terraform Enterprise provides centralized remote state/workspaces, access controls, collaboration and state management around runs.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 71. Difference between terraform plan and apply?

`plan` previews changes. `apply` executes the changes.

```bash
terraform plan
terraform apply
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 72. Which command performs a dry run?

```bash
terraform plan
```

It evaluates the configuration and shows the proposed changes without applying them.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 73. What happens if terraform apply fails after creating some resources?

Terraform records successful changes in state as appropriate and the next plan reconciles the desired configuration with actual infrastructure. Investigate the error before rerunning.

```bash
terraform plan
terraform apply
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 74. Apply failed and state is inconsistent. How do you recover?

First stop blind retries. Check the Azure resources and state, inspect the failed run/logs, run a refresh-aware `plan`, import resources if they exist but are unmanaged, and repair state only with controlled state commands.

```bash
terraform plan
terraform state list
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 75. How do you troubleshoot a failed Terraform deployment?

```text
1. Check pipeline/log error
2. Run terraform validate
3. Review terraform plan
4. Check provider/API permissions
5. Check Azure resource dependencies
6. Check state/locks
7. Fix root cause
8. Run plan again
9. Apply after verification
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 76. How do you monitor Terraform deployment failures?

Use CI/CD logs, Terraform run history, centralized logging/monitoring, alerts, and pipeline status notifications.

```text
Pipeline -> Terraform -> Logs -> Monitoring -> Alert
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 77. How does Terraform identify resource dependencies?

Terraform builds a dependency graph from references between resources. It also supports explicit dependencies through `depends_on`.

```hcl
resource "azurerm_subnet" "subnet" {
  virtual_network_name = azurerm_virtual_network.vnet.name
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 78. What is depends_on?

`depends_on` explicitly tells Terraform that one resource/module must wait for another.

```hcl
resource "azurerm_virtual_machine" "vm" {
  # ...
  depends_on = [
    azurerm_network_interface.nic
  ]
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 79. How does Terraform know RG -> VNet -> Subnet -> NIC -> VM order?

Terraform follows references and builds a dependency graph.

```text
Resource Group
      |
      v
     VNet
      |
      v
    Subnet
      |
      v
     NIC
      |
      v
      VM
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 80. Difference between implicit and explicit dependencies?

Implicit dependency comes from resource references. Explicit dependency is declared with `depends_on`.

```hcl
# Implicit
resource_group_name = azurerm_resource_group.rg.name

# Explicit
depends_on = [azurerm_resource_group.rg]
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 81. Why use terraform import?

It brings an existing resource under Terraform management by associating it with a resource address in state.

```bash
terraform import azurerm_resource_group.rg /subscriptions/SUB/resourceGroups/rg-demo
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 82. How do you import an existing Azure VM?

First define a matching Terraform resource block, then import the Azure resource ID.

```bash
terraform import azurerm_linux_virtual_machine.vm "/subscriptions/SUB/resourceGroups/rg/providers/Microsoft.Compute/virtualMachines/vm01"
```

Then run `terraform plan` and align the configuration with the actual resource.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 83. How do you import manually-created Azure resources?

Define the Terraform resource, find the Azure resource ID, import it, inspect state, and update configuration until `terraform plan` is clean.

```bash
terraform import RESOURCE_ADDRESS RESOURCE_ID
terraform plan
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 84. What is the Terraform Import Block?

An import block allows imports to be declared in Terraform configuration.

```hcl
import {
  to = azurerm_resource_group.rg
  id = "/subscriptions/SUB/resourceGroups/rg-demo"
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 85. Difference between terraform import and data block?

`terraform import` brings an existing resource into Terraform management/state. A `data` block reads existing information without making Terraform responsible for managing that resource.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 86. Which files are required while importing resources?

At minimum, you need a Terraform configuration containing the target resource address and the correct provider configuration. You may then use an import command or import block.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 87. How do you bring a manually-created Azure resource under Terraform management?

```text
Identify resource
     ↓
Write resource block
     ↓
terraform import
     ↓
terraform plan
     ↓
Align configuration
     ↓
Manage through Terraform
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 88. 8 VMs are Terraform-managed and 2 are manual. How do you manage them?

Keep the Terraform-managed VMs under Terraform. For the two manual VMs, either import them if Terraform should own them or leave them outside Terraform and reference them using data sources when appropriate.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 89. How do you migrate ClickOps infrastructure to Terraform?

Inventory resources, classify ownership, create modules/configuration, import existing resources, compare with `plan`, remediate drift, and then move future changes into CI/CD.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 90. What is a Terraform Data Block?

A data block reads information about an existing object without creating/managing that object.

```hcl
data "azurerm_resource_group" "existing" {
  name = "rg-existing"
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 91. When do you use a Data Block?

Use it when Terraform needs information about an existing resource.

```hcl
data "azurerm_resource_group" "existing" {
  name = "rg-existing"
}

resource "azurerm_storage_account" "st" {
  name                     = "stexample123"
  resource_group_name      = data.azurerm_resource_group.existing.name
  location                 = data.azurerm_resource_group.existing.location
  account_tier             = "Standard"
  account_replication_type = "LRS"
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 92. Is a Data Block stored in State?

Data source information can be recorded in Terraform state because Terraform needs the values it read to evaluate the configuration. It does not mean the referenced resource becomes Terraform-managed.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 93. How do you reference an existing Azure resource using a Data Block?

```hcl
data "azurerm_resource_group" "existing" {
  name = "rg-existing"
}

output "rg_location" {
  value = data.azurerm_resource_group.existing.location
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 94. What is Terraform Drift?

Drift occurs when real infrastructure changes outside Terraform and no longer matches the configuration/state Terraform expects.

```text
Terraform Code != Azure Resource
             = Drift
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 95. How do you detect Terraform Drift?

Run:

```bash
terraform plan
```

Terraform compares the desired configuration/state with the current remote object and can show changes caused by external modifications.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 96. What happens if someone manually changes a Terraform-managed resource?

Terraform can detect the difference during refresh/plan. Depending on the configuration, the next apply may change the resource back to the desired configuration.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 97. VM deleted/modified in Azure Portal but exists in Terraform code. What do you do?

Run `terraform plan`, inspect the proposed change, verify the real Azure state, and decide whether Terraform should recreate the resource or the code/state should be changed.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 98. What types of Terraform Drift have you encountered?

Common examples include VM size changes, tags changed in the portal, network/security changes, deleted resources, changed SKU/configuration, and manually modified identities.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 99. How do you safely handle portal changes?

Always review `terraform plan` before apply. Confirm whether the manual change is intended; if it is intended, update Terraform code. If it is not intended, let Terraform restore the desired configuration.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 100. What is the Terraform lifecycle block?

The lifecycle block changes how Terraform handles resource creation, replacement and destruction.

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "rg-prod"
  location = "East US"

  lifecycle {
    prevent_destroy = true
  }
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 101. Explain create_before_destroy.

`create_before_destroy` tells Terraform to create a replacement before destroying the old resource when replacement is required.

```hcl
lifecycle {
  create_before_destroy = true
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 102. What are common lifecycle arguments?

Common lifecycle settings include `create_before_destroy`, `prevent_destroy`, `ignore_changes`, and `replace_triggered_by`.

```hcl
lifecycle {
  prevent_destroy = true
  ignore_changes  = [tags]
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 103. How do you prevent accidental production deletion?

Use lifecycle protections, code review, CI/CD approvals, least privilege, separate state and subscriptions, and explicit change controls.

```hcl
lifecycle {
  prevent_destroy = true
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 104. Can lifecycle rules be used with Storage Accounts?

Yes, where the resource/provider supports the lifecycle behavior.

```hcl
resource "azurerm_storage_account" "prod" {
  # ...

  lifecycle {
    prevent_destroy = true
  }
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 105. What is Terraform Taint?

Taint historically marked a resource for recreation. In modern Terraform workflows, resource replacement is generally preferred through `terraform apply -replace`.

```bash
terraform apply -replace="azurerm_linux_virtual_machine.vm"
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 106. What is terraform taint command?

Older Terraform versions used:

```bash
terraform taint azurerm_linux_virtual_machine.vm
```

Modern practice is to use `-replace` so the replacement intent is part of the plan/apply operation.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 107. How do you redeploy only one corrupted VM?

Use a targeted replacement rather than recreating the entire environment.

```bash
terraform plan -replace="azurerm_linux_virtual_machine.vm"
terraform apply -replace="azurerm_linux_virtual_machine.vm"
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 108. What is the Terraform move block?

A `moved` block tells Terraform that a resource/module address changed without treating it as a delete-and-create operation.

```hcl
moved {
  from = azurerm_resource_group.old
  to   = azurerm_resource_group.new
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 109. How do you move a resource between Terraform state files?

Use controlled state migration techniques such as `terraform state mv` with the appropriate source/destination state/backend, or use import/remove workflows where appropriate.

```bash
terraform state mv   -state-out=other.tfstate   azurerm_resource_group.rg   azurerm_resource_group.rg
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 110. What happens if the Terraform State File is lost?

Terraform loses its mapping between configuration and managed infrastructure. Resources may still exist in Azure, but Terraform may no longer know that it manages them.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 111. How do you recover a deleted State File?

First restore it from backend versioning/backup if available. If no valid state exists, reconstruct management by carefully importing existing resources.

```bash
terraform state list
terraform import RESOURCE_ADDRESS RESOURCE_ID
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 112. How do you handle a corrupted State File?

Stop changes, preserve a copy, restore the last known-good backend version if available, validate the state, and only use advanced state commands after understanding the impact.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 113. Best practices to protect Terraform State?

Use remote state, encryption, RBAC, state locking, versioning, backups, auditing, least privilege, private connectivity where appropriate, and never commit state files to Git.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 114. Can you manually edit Terraform State?

Direct manual editing is risky and generally avoided. Prefer supported commands such as:

```bash
terraform state list
terraform state show RESOURCE
terraform state rm RESOURCE
terraform state mv SOURCE DESTINATION
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 115. How do you remove a resource from state without deleting it?

Use:

```bash
terraform state rm azurerm_linux_virtual_machine.vm
```

This removes Terraform's state tracking for the resource; it does not destroy the Azure resource.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 116. How do you securely manage secrets?

Do not hard-code secrets. Use managed identity/service principals with appropriate permissions, Key Vault or CI/CD secret stores, sensitive variables, and secure state handling.

```hcl
data "azurerm_key_vault_secret" "password" {
  name         = "vm-password"
  key_vault_id = var.key_vault_id
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 117. How do you integrate Terraform with Azure Key Vault?

Store secrets in Key Vault and retrieve them through supported Terraform data sources or use workload identity/managed identity patterns where appropriate.

```hcl
data "azurerm_key_vault" "kv" {
  name                = "kv-prod"
  resource_group_name = "rg-security"
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 118. How do you prevent credentials from being exposed in Terraform?

Use CI/CD secret variables, managed identity/service connections, Key Vault, secret scanning, `.gitignore`, least privilege, and never hard-code passwords in `.tf` files.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 119. Password accidentally committed to GitHub — what do you do?

Immediately rotate/revoke the credential, remove it from the current code, clean repository history if required, scan for further exposure, and ensure the replacement secret comes from a secure secret store.

```text
Rotate -> Revoke old secret -> Remove from repo/history
       -> Scan -> Secure secret storage
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 120. Terraform code is in GitHub. How do you authenticate to Azure?

Prefer workload identity federation/OIDC or another short-lived identity mechanism supported by the CI/CD platform instead of long-lived client secrets.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 121. How do you secure Terraform-based AKS deployments?

Use managed identities, least-privilege RBAC, secure networking, private endpoints/private clusters where required, secret management, policy controls, image/security scanning, and protected CI/CD.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 122. How do you implement Terraform security in CI/CD?

A typical pipeline is:

```text
Terraform fmt
      ↓
Terraform validate
      ↓
TFLint/tfsec/Checkov
      ↓
GitLeaks/TruffleHog
      ↓
Terraform plan
      ↓
Approval
      ↓
Terraform apply
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 123. What is Checkov?

Checkov is an IaC security scanner that checks Terraform and other IaC configurations for policy/security issues.

```bash
checkov -d .
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 124. What is tfsec?

tfsec is a Terraform-focused static security scanner. It identifies insecure configuration patterns.

```bash
tfsec .
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 125. Why use both tfsec and Checkov?

They have overlapping coverage but different rules, checks and policy capabilities. Running both can increase coverage if the team accepts the maintenance and false-positive tradeoffs.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 126. Why use GitLeaks and TruffleHog together?

Both detect exposed secrets, but their detection methods and coverage differ. Using both can provide additional scanning coverage.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 127. Why use SonarQube with IaC security tools?

SonarQube can provide broader code-quality/static-analysis capabilities, while tfsec/Checkov focus more specifically on IaC security policies.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 128. What Terraform security best practices do you follow?

Use remote secured state, least privilege, secret management, provider version pinning, security scanning, code review, protected branches, CI/CD approvals, logging and regular dependency updates.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 129. How do you integrate Terraform with Azure DevOps?

Create pipeline stages for initialization, validation, security checks, plan and controlled apply.

```yaml
steps:
- script: terraform init
- script: terraform validate
- script: terraform plan
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 130. How do you integrate Terraform with GitHub Actions?

Use workflow jobs to install/setup Terraform, authenticate to Azure securely, initialize, validate, scan, plan and apply.

```yaml
- run: terraform init
- run: terraform validate
- run: terraform plan
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 131. How do you connect Terraform to CI/CD?

```text
Developer
   |
 Git
   |
CI Pipeline
   |
Validate/Scan
   |
Terraform Plan
   |
Approval
   |
Terraform Apply
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 132. Write a GitHub Actions Terraform pipeline.

```yaml
name: Terraform

on:
  push:
    branches: [main]

jobs:
  terraform:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: hashicorp/setup-terraform@v3

      - run: terraform init
      - run: terraform fmt -check
      - run: terraform validate
      - run: terraform plan
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 133. How do you manage multiple environments using CI/CD?

Use reusable modules, separate state, environment-specific variables, branch/approval controls and deployment stages.

```text
Dev  -> Automatic
QA   -> Approval
Prod -> Manual Approval
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 134. How do you deploy to multiple Azure subscriptions from one pipeline?

Use provider aliases or separate pipeline jobs/workspaces/states, with secure identity permissions scoped to each subscription.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 135. How do you create 10 Storage Accounts in 10 subscriptions using one pipeline?

Use a map containing subscription-specific configuration and `for_each`, combined with provider aliases or separate provider configurations.

```hcl
variable "storage_accounts" {
  type = map(object({
    subscription_id = string
    name            = string
    location        = string
  }))
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 136. What infrastructure do you provision through Terraform pipelines?

A good answer is: "I provision resources such as resource groups, VNets, subnets, NSGs, route tables, VMs, Storage Accounts, Key Vault, private endpoints, AKS, monitoring components and other Azure services through reusable modules and CI/CD."

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 137. Which Azure services have you created through Terraform?

Common examples include:

```text
Resource Groups
VNets/Subnets
NSGs
Route Tables
VMs
Storage Accounts
Key Vault
Private Endpoints
Load Balancers/Application Gateway
AKS
Monitoring
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 138. How do you automate Azure networking using Terraform?

Create reusable modules for VNets, subnets, NSGs, route tables, NAT, private endpoints and DNS, and pass CIDRs/configuration through variables.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 139. How do you create an Azure VM using Terraform?

A VM typically requires a resource group, network, NIC, image, OS disk and VM resource.

```hcl
resource "azurerm_linux_virtual_machine" "vm" {
  name                = "vm-demo"
  resource_group_name = azurerm_resource_group.rg.name
  location            = azurerm_resource_group.rg.location
  size                = "Standard_B2s"
  admin_username      = "azureuser"
  network_interface_ids = [
    azurerm_network_interface.nic.id
  ]
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 140. Write Terraform code to create an Azure VM.

```hcl
resource "azurerm_linux_virtual_machine" "vm" {
  name                = "vm-demo"
  resource_group_name = azurerm_resource_group.rg.name
  location            = azurerm_resource_group.rg.location
  size                = "Standard_B2s"
  admin_username      = "azureuser"

  network_interface_ids = [
    azurerm_network_interface.nic.id
  ]

  admin_ssh_key {
    username   = "azureuser"
    public_key = file("~/.ssh/id_rsa.pub")
  }

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "0001-com-ubuntu-server-jammy"
    sku       = "22_04-lts"
    version   = "latest"
  }
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 141. How do you create an identical Azure VM?

Create a reusable VM module and pass the required variables.

```text
terraform/
├── main.tf
├── variables.tf
├── outputs.tf
└── modules/
    └── vm/
        ├── main.tf
        ├── variables.tf
        └── outputs.tf
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 142. Application team requests a new VM — end-to-end approach?

```text
Requirement
   ↓
Sizing + Network + Security
   ↓
Module Inputs
   ↓
terraform plan
   ↓
Code Review
   ↓
Approval
   ↓
terraform apply
   ↓
Validation
   ↓
Handover
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 143. How do you deploy an application through Terraform?

Terraform can provision the infrastructure and, where appropriate, application-related resources. For complex application delivery, combine Terraform with deployment tools such as Azure DevOps/GitHub Actions, Helm or Kubernetes tooling.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 144. How would you design a one-click Azure Landing Zone?

Create reusable modules for management groups, subscriptions, networking, identity, policies, logging and security, then orchestrate them from a root module/pipeline.

```text
Landing Zone
├── Management Groups
├── Policies
├── Networking
├── Identity
├── Security
└── Monitoring
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 145. Have you provisioned a complete Azure Landing Zone?

A strong answer is: "Yes, where required I use a modular approach covering governance, management groups/subscriptions, networking, security, identity, policy and monitoring. I keep the landing-zone components reusable and deploy them through controlled CI/CD."

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 146. VM loses Storage Account Private Endpoint connectivity — troubleshoot.

Check:

```text
1. DNS resolution
2. Private DNS Zone/link
3. Private Endpoint NIC/IP
4. NSG rules
5. UDR/route table
6. Azure Firewall/NVA
7. Storage firewall/network rules
8. Port 443
9. VM routing
10. Terraform changes
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 147. How do you verify Private DNS resolution?

From the VM, resolve the Storage Account FQDN and verify it returns the private endpoint IP.

```bash
nslookup <storage-account>.blob.core.windows.net
```

Also verify Private DNS zone links and VNet configuration.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 148. How do NSGs, UDRs, firewall and port 443 affect Private Endpoint connectivity?

NSGs can allow/deny traffic, UDRs can alter routing, firewalls/NVAs can inspect/block traffic, and HTTPS connectivity normally requires TCP 443 to be reachable.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 149. How do you handle multiple Azure Subscription IDs?

Use provider aliases or provider configurations and pass them to the appropriate modules.

```hcl
provider "azurerm" {
  alias           = "dev"
  subscription_id = var.dev_subscription_id
  features {}
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 150. How do you authenticate Terraform across multiple Azure subscriptions?

Authentication is generally established through an Azure identity/service connection, while provider configuration selects the subscription.

```hcl
provider "azurerm" {
  subscription_id = var.subscription_id
  features {}
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 151. How do you pass multiple Subscription IDs to a module?

Pass them as variables or use provider aliases.

```hcl
module "network" {
  source          = "./modules/network"
  subscription_id = var.subscription_id
}
```

For resources in different subscriptions, provider aliases are usually the cleaner approach.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 152. How do you manage remote state for multiple subscriptions?

Keep state isolated per environment/subscription/workload using separate state keys/backends and appropriate access controls.

```text
tfstate/
├── dev.tfstate
├── qa.tfstate
└── prod.tfstate
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 153. What is a Terraform Workspace?

A workspace is a separate state instance associated with the same Terraform configuration.

```bash
terraform workspace list
terraform workspace new dev
terraform workspace select dev
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 154. Why are Terraform Workspaces used?

They allow multiple state instances to use the same configuration. They can be useful for simple environment separation, although larger environments often benefit from separate configurations/state.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 155. Benefits and limitations of Workspaces?

**Benefits:** simple state separation and easy switching.

**Limitations:** can become difficult to manage for highly different environments, permissions, lifecycle controls and complex production architectures.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 156. Workspaces vs separate environment folders?

Use workspaces when configuration is largely identical and only state differs. Use separate environment roots when environments require stronger isolation or significantly different configuration.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 157. Difference between count and for_each?

`count` creates instances based on a number/index. `for_each` creates instances based on a set/map of keys.

```hcl
resource "azurerm_resource_group" "rg" {
  count = 3
  name  = "rg-${count.index}"
}
```

```hcl
resource "azurerm_resource_group" "rg" {
  for_each = toset(["dev", "qa", "prod"])
  name     = "rg-${each.key}"
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 158. When do you use count vs for_each?

Use `count` for simple identical instances. Use `for_each` when each instance has a meaningful stable key or different configuration.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 159. How do for_each, maps, lists and objects work?

A common enterprise pattern is a map of objects:

```hcl
variable "vms" {
  type = map(object({
    size = string
    zone = number
  }))
}
```

Then:

```hcl
for_each = var.vms
size     = each.value.size
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 160. Write Terraform code using a module with for_each.

```hcl
module "vm" {
  source   = "./modules/vm"
  for_each = var.vms

  name = each.key
  size = each.value.size
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 161. What are Terraform Provisioners?

Provisioners execute commands/scripts during resource creation or destruction.

```hcl
provisioner "file" {
  source      = "app.conf"
  destination = "/tmp/app.conf"
}
```

They should generally be avoided when a provider/resource-native mechanism exists.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 162. What is a File Provisioner?

It copies files from the machine running Terraform to a target resource, commonly through SSH/WinRM depending on the provisioner.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 163. Why are Provisioners discouraged?

They can be less predictable, harder to make idempotent, dependent on network/remote access, and less declarative than using native Terraform/provider resources.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 164. What is null_resource?

`null_resource` is a resource that does not represent a real infrastructure object and was historically used to trigger provisioners or command execution.

```hcl
resource "null_resource" "example" {
  triggers = {
    version = var.version
  }
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 165. Practical use case of null_resource?

A legacy example is running a command when a trigger changes. In modern Terraform, prefer `terraform_data` or provider-native resources where suitable.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 166. How do you upgrade a Terraform provider?

Update the provider version constraint and run:

```bash
terraform init -upgrade
```

Then test with:

```bash
terraform plan
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 167. How do you upgrade Terraform versions?

Review release notes, check provider/module compatibility, update version constraints, test in a non-production environment, run validation/plan, and then roll out through CI/CD.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 168. What compatibility checks are required before an upgrade?

Check Terraform language compatibility, provider versions, module constraints, deprecated resources/arguments, backend compatibility, CI/CD runner versions and state migration implications.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 169. How do you handle provider/module version compatibility?

Pin compatible versions and use a lock file.

```hcl
required_providers {
  azurerm = {
    source  = "hashicorp/azurerm"
    version = "~> 4.0"
  }
}
```

Review `.terraform.lock.hcl` changes during upgrades.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 170. If a module changes from version 3 to 4, how does Terraform know?

Terraform uses the module source and version constraint to select the module version. You explicitly change the constraint/source/version as required and then review the plan and module upgrade documentation.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 171. What challenges have you faced during Terraform upgrades?

Typical challenges include deprecated provider arguments, changed resource behavior, module compatibility, state migrations, provider API changes, and unexpected plan differences. I handle them through testing, version pinning and controlled rollout.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 172. Terraform deployment takes one hour. How do you optimize it?

Review the dependency graph, unnecessary resources, module design, API throttling, `-parallelism`, data sources and CI/CD stages. Split very large state where justified.

```bash
terraform plan -parallelism=20
```

Test before increasing concurrency in production.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 173. How does parallelism improve Terraform performance?

Terraform can execute independent operations concurrently.

```bash
terraform apply -parallelism=20
```

The value should be tuned against provider/API throttling and resource dependencies.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 174. How do you optimize a large Terraform project?

Use modular architecture, separate state boundaries where appropriate, avoid unnecessary dependencies, use `for_each` effectively, control parallelism, reduce expensive data lookups, and optimize CI/CD.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 175. Explain a real-time Terraform deployment failure.

A strong structure is:

```text
Problem -> Impact -> Investigation -> Root Cause -> Fix -> Prevention
```

Example: "A deployment failed because the pipeline identity lacked permission to create a network resource. I checked the Terraform error and Azure activity logs, corrected RBAC, reran plan, verified the change and then applied."

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 176. Explain one real-time Terraform issue you fixed.

Use a concrete STAR-style answer:

```text
Situation: Deployment was failing.
Task: Identify the root cause.
Action: Checked plan, provider logs, Azure RBAC and dependencies.
Result: Corrected the configuration/permission and redeployed successfully.
Prevention: Added validation and pipeline checks.
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 177. Terraform accidentally deleted Application Gateway. What do you do?

Stop further changes, inspect the plan/state and Git change, determine why Terraform believed replacement/deletion was required, recover the resource if necessary, and add lifecycle/change-control protections.

```hcl
lifecycle {
  prevent_destroy = true
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 178. Someone manually changed VM size. What happens during plan?

If the VM's configured size differs from the desired Terraform configuration, `terraform plan` can show a change to reconcile the infrastructure with the configuration.

```bash
terraform plan
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 179. Office manually installed on a Terraform VM — what happens on apply?

Terraform generally manages declared infrastructure attributes, not arbitrary software installed manually inside the VM. Installing Office manually does not automatically make Terraform remove it unless a managed configuration/provisioning mechanism explicitly controls it.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 180. Custom image software updated — what happens on apply?

If Terraform's configuration still references the same image/version identifier and no managed attribute changed, Terraform may not automatically recreate the VM simply because software inside an image changed. Image/version changes that alter the resource configuration can trigger replacement depending on the resource.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 181. Resource deleted from Azure Portal — how do you recover?

Run:

```bash
terraform plan
```

If Terraform still expects the resource, the plan may propose recreation. Verify dependencies and whether recreation is safe before applying.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 182. Two teams deploy to the same Azure subscription. How do you manage it?

Use clear state boundaries, ownership, RBAC, remote state locking, reusable modules, separate pipelines, code review and change controls.

```text
Team A -> State A
Team B -> State B
Shared resources -> Controlled ownership
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 183. Difference between plan and apply?

```bash
terraform plan   # Preview
terraform apply  # Execute
```

Plan should be reviewed before applying production changes.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 184. Which command shows Terraform state/resource information?

```bash
terraform state list
terraform state show azurerm_resource_group.rg
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 185. How do you get VM output in JSON?

```bash
terraform show -json
```

If you specifically want state as JSON:

```bash
terraform show -json terraform.tfstate
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 186. Which commands are used to manage Terraform State?

```bash
terraform state list
terraform state show RESOURCE
terraform state mv SOURCE DESTINATION
terraform state rm RESOURCE
terraform state pull
terraform state push
```

Use state commands carefully, especially in production.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 187. How do you remove a resource from Terraform State?

```bash
terraform state rm azurerm_linux_virtual_machine.vm
```

This removes the state entry; it does not delete the Azure resource.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 188. Which command force-unlocks Terraform State?

```bash
terraform force-unlock LOCK_ID
```

Only use it after verifying the lock is stale.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 189. What Terraform best practices do you follow?

I use reusable modules, remote state, state locking, provider/version pinning, CI/CD, code review, security scanning, secret management, separate environments/state, documentation and least privilege.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 190. How do you ensure Terraform follows DRY?

Avoid copying resource definitions across environments. Put common infrastructure into modules and use variables, locals, maps and `for_each`.

```hcl
module "storage" {
  source   = "./modules/storage"
  for_each = var.storage_accounts
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 191. How do you make Terraform reusable, secure and scalable?

Use modular architecture, versioned modules, typed variables, outputs, remote state, secure authentication, policy/security scanning, CI/CD, testing and clear state boundaries.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 192. How do you standardize Terraform across teams?

Use a module registry, coding standards, version constraints, CI/CD templates, security policies, reusable pipeline components, documentation and mandatory review.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 193. How do you separate infrastructure ownership?

Separate state and modules by ownership boundaries. Define which team owns each resource and prevent multiple Terraform states from managing the same resource.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 194. How do you design Terraform for enterprise scale?

I use:

```text
Reusable Modules
      +
Separate State Boundaries
      +
Remote Backend
      +
CI/CD
      +
Security Scanning
      +
RBAC
      +
Version Pinning
      +
Governance
```

The goal is predictable, auditable and repeatable infrastructure.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 195. What Terraform projects have you worked on?

Answer with your real experience. A strong structure is:

```text
Project
  -> Business requirement
  -> Azure services
  -> Terraform modules
  -> CI/CD
  -> Security
  -> State management
  -> Result
```

Avoid claiming technologies you have not actually used.

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 196. What Terraform modules have you worked on?

Explain the actual modules you have built. Common examples include networking, VMs, Storage, Key Vault, AKS, monitoring and security.

```text
modules/
├── network
├── vm
├── storage
├── keyvault
└── aks
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 197. How many reusable Terraform modules have you created?

Give your actual number. Then explain the most important modules and why they were reusable.

```text
Module -> Inputs -> Resources -> Outputs
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 198. Have you created Terraform infrastructure from scratch?

A good answer structure is:

"Yes. I start with provider/backend configuration, define the infrastructure architecture, build reusable modules, add variables/outputs, validate and scan the code, create the plan, review it, and deploy through CI/CD."

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 199. What infrastructure is provisioned through your Terraform pipelines?

Mention only what you have actually worked with. Typical examples are:

```text
Azure Resource Groups
VNets/Subnets
NSGs
VMs
Storage
Key Vault
Private Endpoints
AKS
Application Gateway
Monitoring
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 200. Which latest Terraform/AzureRM provider version have you worked with?

Answer with the exact version you have actually used in your project. Do not guess a version in an interview.

```hcl
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "YOUR_TESTED_VERSION"
    }
  }
}
```

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 201. Rate yourself in Terraform out of 10.

Give an honest rating and justify it with practical skills.

**Example:**

"I would rate myself 8/10. I am comfortable with Azure infrastructure, modules, state management, CI/CD, troubleshooting, security and production deployments. I am continuously improving advanced Terraform architecture and ecosystem knowledge."

---

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

### 202. Explain your most challenging Terraform production issue and how you solved it.

Use this interview structure:

```text
1. Situation
   What infrastructure/project was involved?

2. Problem
   What exactly failed?

3. Investigation
   What did you check?
   - terraform plan
   - state
   - provider logs
   - Azure Activity Logs
   - RBAC
   - dependencies

4. Root Cause
   What was actually causing the issue?

5. Solution
   What change did you make?

6. Validation
   How did you confirm the fix?

7. Prevention
   What did you change in CI/CD, modules,
   security or monitoring so it would not happen again?
```

**Interview example:**

"A Terraform deployment failed in production because a required Azure permission was missing. I first reviewed the pipeline error and Terraform plan, then checked Azure Activity Logs and RBAC assignments. I identified that the deployment identity did not have the required permission. After correcting the RBAC assignment, I reran `terraform plan`, verified that the expected changes were shown, and then applied the deployment. Finally, I added permission validation and pipeline checks to reduce the chance of the issue recurring."

---

## 🔥 Top 30 Terraform Questions You Must Prepare

If you have limited interview-preparation time, focus first on these:

1. What is Terraform?
2. Terraform workflow
3. Terraform architecture
4. Provider
5. Root vs Child Module
6. Reusable Modules
7. Resource vs Pattern Module
8. Variables and Data Types
9. `count` vs `for_each`
10. Data Block
11. Terraform State File
12. Remote State
13. State Locking
14. `terraform force-unlock`
15. State corruption/recovery
16. Terraform Drift
17. Drift detection/resolution
18. `terraform plan` vs `apply`
19. Dependencies
20. `depends_on`
21. Terraform Import
22. Import Block
23. Lifecycle
24. `prevent_destroy`
25. `create_before_destroy`
26. Terraform Workspaces
27. Terraform CI/CD
28. Terraform + Azure Key Vault
29. Terraform security: tfsec/Checkov/GitLeaks
30. Real-time Terraform troubleshooting

> 💡 **Master Terraform with hands-on training — ₹999 | Lifetime Access** → https://www.cloudbloggeracademy.com/courses/Terraform--6a6a05ca43b9521db1eb6cca

