## Module types and versioning: Modularize your Terraform code [WIP]

Modules are a great way of keeping your code tight, readable and mantainable. They also offer a logical way of keeping up your Terraform code aligned with the application architecture by mirroring its structure. This provides a great reading experience when switching between application and infrastructure code, as for each app codebase there is an infra counterpart that pairs with it.

There are essentially four major types of modules that may have different versioning paths:
- shared modules
- component modules
- product modules
- environment/config modules

### Versioning Shared modules

Shared modules are resource

### Versioning Component modules

The component layout should follow a meaningful structure, such as the technical or functional view of a project with the former being preferred as it tends to have a more natural resource transposition to Terraform.

We have therefore a one-to-one mapping of view components to Terraform modules. There can be some exceptions in which we may have one view component being represented by multiple Terraform modules that act as a subcomponents of the main one. This can be done if it makes sense from a view and Terraform modularization perspectives.

As the name states, component modules are usually apart of something bigger. Alongside other components, they tend to shape what in the end we call a product, a logical set of resources that work together to produce a certain functionality.

Component modules reside in dedicated repositories and are versioned separately to facilitate its usage adaptability across different product releases. Besides the reusability benefits you also get reduced blast radius as you keep modules simple and versioned, disaster discovery and containment becomes easier to manage.

Common use cases:

- Typical multi-tier web applications
- Microservices architectures

### Versioning Product modules


### Versioning Environment modules

### How to version: Git tags + Semantic Versioning

The actual task of versioning a module follows the same approach of any other git repository. Ideally, version increments are made programmatically alongside the [Semantic Versioning Specification](https://semver.org/).