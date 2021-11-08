# State management and modularization: How to structure your Terraform projects [WIP]

State management should follow a decentralized pattern. The benefits obtained with this type of approach are immense: reduced complextity, faster executions, reduced blast radius, easier drift management, isolation between components and teams.

## Workspaces: Yes or No ?

TL;DR Workspaces are NOT recommended if you're using the Terraform CLI. 

Many guides give high praises to Terraform Workspaces as the way for structuring your components or environment stages, and this is all true IF you are using Terraform Cloud. Unfortunately the Terraform Cloud and CLI share different concepts of Workspaces, which you can see in more detail [here](https://www.terraform.io/docs/cloud/workspaces/index.html).

This means that for most use cases there are better alternatives to workspaces when using the Terraform CLI. The CLI's workspaces are a good choice for managing multi-tenancy use cases out of a single codebase such as regions, teams or environment stages. However more frequently that not, tenants usually digress in their configurations whether its business or security restrictions, technical limitations or even the nature of the tenancy types applied. In these scenarios it's a much better approach to manage the tenants in separate configurations.

## The `terraform_remote_state` data source

The [`terraform_remote_state`](https://www.terraform.io/docs/language/state/remote-state-data.html) data source is the best way to access and share resources between different terraform states. This is due to the fact that a state file belongs to a single Terraform backend and in component-centric structures there is usually the need to access resources from different components thus states.

## Project structure

This section assumes you have already read the [modularization documentation](./MODULARIZATION.md).

Ideally your project's infrastructure should be mapped following your applications structure approach. Typical microservices architectures are easily mapped in the infrastructure side of things but there are some specific cases and resources that are not that easy to assign to a particular module or component. In such cases you can either go one level higher in the hierarchy to be able to include those resources or in most cases, create a separate, shared **utilities module**.

### Utilities modules

Utility or support modules (there isn't a general consensus about how to name them) are the best approach to place resources that are not easily translatable from the application architecture or other technical. Network, Database and User Management are amongside many others, resources that are tipically absent from the application architecture whose focus is geared towards its core. Backbone oriented resources such as the ones mentioned do not fit the standard mapping strategy and should instead be assigned to these utilities modules (or whatever it is you prefer to call them) that offer a good solution for grouping these types of resources into something meaninful without sacrificing the benefits of using modularization.

If you infra development is in pair with the application development you will general start with a simple setup that won't require you to do much around organizing and you should be able to manage all off of one single repository and configuration. As the project develops and grows, so will its complexity and it will eventually start to make sense to move from a monolithic approach into something a bit more modular and properly organized, but this is all part of a continuous and evolutive process in improving code quality.

If however your application stack is already well defined and mature and you just started the the integration of IaC into the project then everything should be defined upfront before jumping into action.