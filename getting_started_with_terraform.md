# Getting Started with Terraform

Terraform is an [infrastructure as code (IaC)](https://www.terraform.io/docs/glossary#infrastructure-as-code) tool that allows you to build, change, and version infrastructure safely and efficiently. 

## Prerequisites
 
 - [Docker](https://www.docker.com/)
 - [Terraform](https://www.terraform.io/downloads.html) 
 
## Create a configuration file.
you will create a file named main.tf  This file contains the configuration of the resources to deploy a Ngnix docker container.  

We recommend crreating a directory for your configuration file.
```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}

#configure the docker provider
provider "docker" {
    host = "unix:///var/run/docker.sock"
}

# Create a docker container resource
# -> same as 'docker run --name nginx -p8080:80 -d nginx:latest'

  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}

# Create a docker image resource
# -> docker pull nginx:latest
resource "docker_container" "nginx" {
  image = docker_image.nginx.repo_digest

resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Initialize Terraform with the `init` command. The AWS provider will be installed. 

```shell
$ terraform init
```

You shoud check for any errors. If it ran successfully, provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command will take up to a few minutes to run and will display a message indicating that the resource was created.

Finally, destroy the infrastructure.

```shell
$ terraform destroy
```

Look for a message are the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it had created earlier.