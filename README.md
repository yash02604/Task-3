# Task 3: Infrastructure as Code (IaC) with Terraform

## Objective
Provision a local Docker container using Terraform.

## Tools
- Terraform
- Docker Desktop
- Docker provider for Terraform
- Nginx Docker image

## What I did
1. Verified Terraform and Docker installation.
2. Created a Terraform configuration using the Docker provider.
3. Ran `terraform init`.
4. Ran `terraform plan` and verified that Terraform planned 2 resources:
   - `docker_image.nginx`
   - `docker_container.nginx`
5. Ran `terraform apply`.
6. The first apply attempt could not bind host port 8080 because a Java process was already listening on that port.
7. Changed the host port from 8080 to 8081 while keeping the Nginx container port at 80.
8. Ran `terraform apply` again successfully.
9. Verified the container with Docker and opened `http://localhost:8081`.
10. Checked Terraform state using `terraform state list` and `terraform state show docker_container.nginx`.
11. Ran `terraform destroy` successfully. Terraform reported: `Resources: 2 destroyed.`

## Port Mapping

```text
Host:      8081
             |
             v
Container: 80
             |
             v
           Nginx
```

The Nginx welcome page was successfully accessible at:

`http://localhost:8081`

## Terraform Resources

- `docker_image.nginx` — pulls/manages `nginx:latest`
- `docker_container.nginx` — creates the `terraform-nginx` container

## Important Terraform Commands

```powershell
terraform init
terraform plan
terraform apply
terraform state list
terraform state show docker_container.nginx
terraform destroy
```

## Result

The task demonstrated the Terraform IaC lifecycle:

```text
Configuration
     ↓
terraform init
     ↓
terraform plan
     ↓
terraform apply
     ↓
Docker container running
     ↓
Verify application
     ↓
terraform state
     ↓
terraform destroy
```


