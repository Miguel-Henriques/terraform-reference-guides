# Git Workflows for Terraform : Choosing your branching strategy

Branching strategy and Git Workflow are interchangeably used.

The standard and most well known branching practices can generally be applied to Terraform repositories however and like in any language it's all subjective, there is no such thing as a silver bullet for branching.

It also varies based on the type of Terraform repository you're handling, for module repositories there's usually some sort release process and well defined versioning, whereas with config repositories there's at most some short-lived features branches as a two-step integration of configuration changes or new additions without breaking live production infrastructure provisioning that sits on the master branch (Feature Branch Workflow). With some config repositories you can entirely skip the need for separate branches and work all in the trunk (master branch) as most of the time you will be just adding new and completely isolate environments that do not impact in any way the existing environments.

You can use this cheatsheet as guide:

| Repository type | Git Workflow  |
| -               | -             |
| Config  | Trunk based development / Centrallized |
| Module(*)  | Gitflow / Github Flow |

(*) Here are included the following: **shared**, **component** and **product** modules

A reminder that it all comes up to what best fits **your** needs and it's completely acceptable that you end up switching workflows, mixing them up or even opting for other ones that weren't mentioned such as the Forking Workflow.