# Getting Started with Terraform

Terraform is an [infrastructure as code (IaC)](https://www.terraform.io/docs/glossary#infrastructure-as-code) tool that allows you to build, change, and version infrastructure safely and efficiently. 

## Requirements
 
 - [Docker](https://www.docker.com/)
 - [Terraform](https://www.terraform.io/downloads.html) 
 
## Create Infrastructure Resources
you will create a file named main.tf  This file contains the configuration of the resources to deploy a Ngnix docker container.  

Create a directory named _terraform-demo_.

```shell
$ mkdir terraform-demo
```
Then, go to this directory.
```shell
$ cd terraform-demo
```


Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following Terraform configuration into the file.

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
# -> same as 'docker run --name training -p80:80 -d nginx:latest'

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

## Deploy Infrastructure Resources
Initialize Terraform, which downloads a plugin that allows the project to run Docker. 

```shell
$ terraform init
```


Provision the NGINX webserver with ***_terraform apply_***.  Enter ***_yes_***, then press ***_ENTER_*** when prompted.

```shell
$ terraform apply
```

Verify the docker container is running. 
```shell
$ docker ps -a
```
<image title="Docker Process Check" alt="Docker Process Check" src="images/docker-ps-output.jpg">


Verify the webserver is accessible.
```shell 
$ curl localhost:80
```
<image title="Curl Webserver" alt="Curl Webserver" src="images/lnx-curl-localhost.jpg">

## Remove Infrastructure Resources

To remove the container type ***_terraform destroy_*** .

```shell
$ terraform destroy
```

To complete the removal, type ***_yes_*** and press ***_ENTER_***. Terraform will destroy the resources it had created earlier.

You have now depolyed and destroyed webserver with Terraform.
