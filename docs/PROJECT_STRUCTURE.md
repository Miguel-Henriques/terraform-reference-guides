# State management and modularization: How to structure your Terraform projects [WIP]

State management should follow a decentralized pattern. The benefits obtained with this type of approach are immense: reduced complextity, faster executions, reduced blast radius, easier drift management, isolation between components and teams.

## Workspaces: Yes or No ?

TL;DR Workspaces are NOT recommended if you're using the Terraform CLI. 

Many guides give high praises to Terraform Workspaces as the way for structuring your components or environment stages, and this is all true IF you are using Terraform Cloud. Unfortunately the Terraform Cloud and CLI share different concepts of Workspaces, which you can see in more detail [here](https://www.terraform.io/docs/cloud/workspaces/index.html).

This means that for most use cases there are better alternatives to workspaces when using the Terraform CLI. The CLI's workspaces are a good choice for managing multi-tenancy use cases out of a single codebase such as regions, teams or environment stages. However more frequently that not, tenants usually digress in their configurations whether its business or security restrictions, technical limitations or even the nature of the tenancy types applied. In these scenarios it's a much better approach to manage the tenants in separate configurations.