# Module versioninig

There are essentially four major types of modules that may have different versioning paths:
- shared modules
- component modules
- product modules
- environment/config modules

## Versioning Shared modules

Shared modules are resource

## Versioning Component modules

The component layout should follow a meaningful structure, such as the technical or functional view of a project with the former being preferred as it tends to have a more natural resource transposition to Terraform.

A component should therefore be a one-to-one representation of a view component. 

As the name states, component modules are usually apart of something bigger. Alongside other components, they tend to shape what in the end we call a product, a logical set of resources that work together to produce a certain functionality.

Component modules reside in dedicated repositories and are versioned separately to facilitate its usage adaptability across different product releases.

Examples:

1. A typical 3 tier web application:

- Presentation
- Business logic
- Database

2. 