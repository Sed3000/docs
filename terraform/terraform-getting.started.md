## Getting Started with [Terraform](https://www.terraform.io/docs/glossary#terraform)

Terraform is an [infrastructure as code (IaC)](https://www.terraform.io/docs/glossary#infrastructure-as-code) tool that allows you to build, change, and version infrastructure safely and efficiently. 


### Overview

In the demonstration, you will learn how to use Terraform to deploy a container using the docker [provider](https://www.terraform.io/docs/glossary#terraform-provider). A provider is a plugin for Terraform that makes a collection of related resources available. You will complete the following tasks:



1. Install Terraform
2. Create a Terraform Configuration
3. Initialize the Terraform Configuration
4. Deploy a Docker Container
5. Verify the Docker Deployment
6. Remove the Docker Container


### Requirements

Install docker before configuring Terraform.

[Docker](https://docs.docker.com/engine/install/) 


### Install Terraform

Terraform supports Linux, Mac, Windows, and Unix platforms.  [Download](https://www.terraform.io/downloads) and [install](https://learn.hashicorp.com/tutorials/terraform/install-cli) on Terraform.



<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: undefined internal link (link text: "Linux/Unix"). Did you generate a TOC? </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

[Linux/Unix](#heading=h.85s5g7dyd6xj)



<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: undefined internal link (link text: "Windows"). Did you generate a TOC? </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>

[Windows](#heading=h.nh8f0vyygshf)


### Linux


### Create a Terraform Configuration

Create a file for your Terraform configuration:

**Pro Tip:** Create a new directory to create Terraform configuration code inside.


```
$ mkdir terraform-demo
$ cd terraform-demo 
```



```
$ touch main.tf
Paste the following lines into the file.

terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.repo_digest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```


Initialize Terraform with the init command. The docker provider will be installed,


#### Initialize Terraform

Using the **_terraform init_** command, defines the infrastructure resources using code.


```
$ terraform init
```



#### Provisioning Resources

Using the **_terraform apply_** command, deploys the infrastructure resources requested.


```
$ terraform apply 
```



##### Testing deployment

docker command:


```
$ docker ps -a 
```


Output:



<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")


Access the Nginx Web Server on Localhost on TCP port 80.

Linux command:


```
$ curl localhost:80
```


Output:



<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")



#### Removing Resources

Using the**_ terraform destroy_**, You will delete the infrastructure resources provisioned.


```
$ terraform destroy
```


Look for a message are the bottom of the output asking for confirmation. Type **_yes_** and hit **ENTER**. Terraform will destroy the created resources.


### Windows


### Create a Terraform Configuration

Create a file for your Terraform configuration:

**Pro Tip:** Create a new directory to create Terraform configuration code inside.



<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.png "image_tooltip")



```
> notepad main.tf
Paste the following lines into the file.

terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "npipe:////.//pipe//docker_engine"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.repo_digest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```


Initialize Terraform with the init command. The docker provider will be installed,


#### Initialize Terraform

Using the **_terraform init_** command, defines the infrastructure resources using code.


```
> terraform init
```


Output



<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.png "image_tooltip")



#### Provisioning Resources

Using the **_terraform apply_** command, deploys the infrastructure resources requested.


```
> terraform apply 
```



##### Testing deployment

docker command:


```
> docker ps -a 
```


Output:



<p id="gdcalert7" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image5.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert8">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image5.png "image_tooltip")


Access the Nginx Web Server on Localhost on TCP port 80.

Linux command:


```
> curl localhost:80
```


Output:



<p id="gdcalert8" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image6.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert9">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image6.png "image_tooltip")



#### Removing Resources

Using the**_ terraform destroy_**, You will delete the infrastructure resources provisioned.


```
> terraform destroy
```


Look for a message are the bottom of the output asking for confirmation. Type **_yes_** and hit **ENTER**. Terraform will destroy the created resources.