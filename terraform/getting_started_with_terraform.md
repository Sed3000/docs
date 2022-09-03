# Getting Started with Terraform

Terraform is an [infrastructure as code (IaC)](https://www.terraform.io/docs/glossary#infrastructure-as-code) tool that allows you to build, change, and version infrastructure safely and efficiently. 

To install Terraform, see Requirements section.

## Requirements
 
 - [Docker](https://www.docker.com/)
 - [Terraform](https://www.terraform.io/downloads.html) 
 
## Create Infrastructure Resources
 You will create a configuration file of the resources to deploy a Ngnix docker container.  

1. Create a  _terraform-demo_ directory.

```shell
$ mkdir terraform-demo
```
2. Navigavte to the _terraform-demo_ directory.
```shell
$ cd terraform-demo
```


3. Create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

4. Paste the following Terraform configuration into the file.

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
1. Initialize Terraform. 
This command downloads a plugin that lets the project run Docker. 

```shell
$ terraform init
```

	Terraform has successfully initialized

<image>

2. Deploy the NGINX webserver with ***_terraform apply_***.  
```shell
$ terraform apply
```
<image>

3. Type ***_yes_*** when prompted, press ***_ENTER_***.

<image>

Terraform has successfully provisioned resources.

4. Type the following command to cconfirm the docker container is running. 
```shell
$ docker ps
```
<image title="Docker Process Check" alt="Docker Process Check" src="images/docker-ps-output.jpg">


5. Type the following command to confirm the webserver is running.
```shell 
$ curl localhost:80
```
<image title="Curl Webserver" alt="Curl Webserver" src="images/lnx-curl-localhost.jpg">


## Remove Infrastructure Resources

1. Type ***_terraform destroy_***  to remove resources.

```shell
$ terraform destroy
```

2. Type ***_yes_*** , when prompted, press ***_ENTER_***. 
Terraform will destroy the resources previously created.
<image>

Congratulations, You have deployed a Webserver using Docker and Ngnix with Terraform.

## Resources

<other links>
