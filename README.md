# Overview

Hashicorp doesn't recommend using multiple workspaces when needed to isolate applications and its state. Instead it's recommended to separate configuration for each envrionment so that you can represent the differences between your environments in a straightfoward and readable way.

For elements that are common between the environments, you can use a shared modules to represent those and call those modules in a different way for each environment.

## Automation

Terraform does not currently have any built-in ways to cascade runs from one configuration to another. Teams that have architectures like this will run [Terraform in automation](https://learn.hashicorp.com/terraform/development/running-terraform-in-automation) and then use automation for cascading runs.

Sources:
* [Hashicorp](https://learn.hashicorp.com/terraform/development/running-terraform-in-automation)
* [Response](https://discuss.hashicorp.com/t/way-to-work-with-directory-structure/3698/4)

Folder layout

```
└── terraform-structure
    ├── README.md
    └── example
        ├── environment
        │   ├── dev  # dev configuration
        │   │   └── dev.tf 
        │   └── prod # prod configuration
        │       └── prod.tf
        └── modules
```

Then `environment/prod/prod.tf` will look like this.

```
terraform {
    backend "gcs" {
        bucket = "tf-state-prod"
        prefix = "terraform/state"
    }
}
```