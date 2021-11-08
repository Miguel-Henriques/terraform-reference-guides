## Module types and versioning: Modularize your Terraform code

Modules are a great way of keeping your code tight, readable and mantainable. They also offer a logical way of keeping up your Terraform code aligned with the application architecture by mirroring its structure. This provides a great reading experience when switching between application and infrastructure code, as for each app codebase there is an infra counterpart that pairs with it.

There are essentially four major types of modules that may have different versioning paths:

- shared modules
- component modules
- product modules
- environment/config modules

### Shared modules

Shared or common modules are general purpose modules that provide extensive configurability. These modules are essentially time saving solutions for common project/team/organization use cases that reduce the amount of possibly duplicate code you would have if you were not using them, as well as saving time developing and maintaining this same codebase.

Other major benefit of using these modules is increased confidence and predictability, specially if you are using modules of verified or generally accepted/trusted providers, such as Terraform's official providers or even your own org's providers. In most big organizations there is one or more DevOps departments that have an IaC stack composed of multiple modules which they publish themselves within the org or publicly. These stacks tend to be continuosly improved to be up to date with newest features and tested to comply with performance and security requirements.

So, everytime you want to do something in Terraform the first thing you should ask yourself is: is there any existing module that suits this? Because most likely there is. And if that existing module is not quite what you wanted because you need some extra features, you can built on top of that thanks to Terraform module composeability, just create a module on top of that module that fills those gaps and you are good to go.

A shared module should have a clearly defined scope, its naming should be indicative of its functionality and it shouldn't try to do more than it is supposed to. A shared module can have module dependencies i.e. use other shared modules.

Examples:

- Application module: Provides the blueprint for deploying an application within a project
- Tag module: Creates a list of tags following the organization's scheme

### Component modules

The component layout should follow a meaningful structure, such as the technical or functional view of a project with the former being preferred as it tends to have a more natural resource transposition to Terraform.

We have therefore a one-to-one mapping of view components to Terraform modules. There can be some exceptions in which we may have one view component being represented by multiple Terraform modules that act as a subcomponents of the main one. This can be done if it makes sense from a view and Terraform modularization perspectives.

As the name states, component modules are usually apart of something bigger. Alongside other components, they tend to shape what in the end we call a product, a logical set of resources that work together to produce a certain functionality.

Component modules reside in dedicated repositories and are versioned separately to facilitate its usage adaptability across different product releases. Besides the reusability benefits you also get reduced blast radius as you keep modules simple and versioned, disaster discovery and containment becomes easier to manage.

Common use cases:

- Typical multi-tier web applications
- Microservices architectures

### Product modules

Product modules refer to the stacks that make for the products infrastructure provisioning. They're generally made of a composition of component modules, initialized with the product specific configurations although this is not a strict requirement as in some cases the product isn't split into components, either because it doesn't make sense to do so (rarely) or more commonly during initial development stages for simplicity purposes. As the product grows in complexity it tends to make sense to start spliting things into modules to maintain readibility.

### Environment modules

Environments are nothing more than product instances. These do not apply to every scenario but rather to multi-tenant distributions with dedicated infrastructure. For multi-tenancy products hosted on shared infrastructure the product module is sufficient as there is no tenant-specific configurations to define.

Environment modules should NOT include any Terraform configuration besides the terraform backend initialization and product configuration.

Example:

```
├── environment #1  
│   ├─ main.tf  
│   └─ env.tfvars  
├── environment #2  
│   ├─ main.tf  
│   └─ env.tfvars 
``` 

In some cases it may be advisable to create sub-environments, for example the multiple environment stages of a specific tenant, while retaining tenant-wide variables as such:

```
├─ environment #1  
│  ├─ dev  
│  │  ├─ main.tf  
│  │  └─ env.tfvars  
│  ├─ int  
│  │  ├─ main.tf  
│  │  └─ env.tfvars  
│  ├─ prod  
│  │  ├─ main.tf  
│  │  └─ env.tfvars  
│  ├─ main.tf  
│  └─ global.tfvars
├─ environment #2  
│  ├─ main.tf  
│  └─ env.tfvars  
```


### How to version: Git tags + Semantic Versioning

The actual task of versioning a module follows the same approach of any other git repository. Ideally, version increments are made programmatically either leveraging your SCM capabilities, as part of your CI pipelines or even relying on less elegant solutions such as traditional bash scripts. You should base your versioning on a well defined open standard such as the [Semantic Versioning Specification](https://semver.org/).