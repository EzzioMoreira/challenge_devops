## DevOps Challenge
![Diagram](https://github.com/EzzioMoreira/challenge_devops/blob/main/img/diagram.JPG)
![App-Rapadura](https://github.com/EzzioMoreira/challenge_devops/blob/main/img/proxy.JPG)
#### Clone the Repositories used in this project
- [AWX](https://github.com/EzzioMoreira/awx.git)
- [Packer for AMI AWX](https://github.com/EzzioMoreira/packer-rapadura-awx.git)
- [EC2 APP WEB](https://github.com/EzzioMoreira/ec2-rapadura.git)
- [EC2 AWX](https://github.com/EzzioMoreira/awx-rapadura.git)
- [AWS RDS MySQL](https://github.com/EzzioMoreira/rds-terraform.git)
- [Playbooks Ansible for website](https://github.com/EzzioMoreira/web-rapadura.git)

#### 1. Criar imagem AWS AMI para AWX.
```shell
# run container
docker run -it -v $PWD:/app -w /app --entrypoint "" hashicorp/packer:light sh
# install ansible
apk -U add ansible
# environments ima aws
export AWS_ACCESS_KEY_ID=your_key_here
export AWS_SECRET_ACCESS_KEY=your_secret_key_here
export AWS_DEFAULT_REGION=your_region_here
# run docker create artefact
packer build app.json.pkr.hcl
```
#### 2. Create EC2 for web application
```make
# set your credentials to aws in the .env file
AWS_ACCESS_KEY_ID=your_key_here
AWS_SECRET_ACCESS_KEY=your_secret_key_here
# Run terraform init to download all necessary plugins
make terraform-init
# Exec a terraform plan and puts it on a file called plano
make terraform-plan
# Uses plano to apply the changes on AWS.
make terraform-apply
# Destroy all resources created by the terraform file in this repo.
make terraform-destroy
# we need output for acces website
rapadura-public_dns = "ec2-54-215-226-216.us-west-1.compute.amazonaws.com"
```

#### 3. Create EC2 for Ansible AWX
```make
# set your credentials to aws in the .env file
AWS_ACCESS_KEY_ID=your_key_here
AWS_SECRET_ACCESS_KEY=your_secret_key_here
# Run terraform init to download all necessary plugins
make terraform-init
# Exec a terraform plan and puts it on a file called plano
make terraform-plan
# Uses plano to apply the changes on AWS.
make terraform-apply
# Destroy all resources created by the terraform file in this repo.
make terraform-destroy
# Access AWX:
awx-rapadura-public_dns: "ec2-54-67-82-124.us-west-1.compute.amazonaws.com"
User: admin
Password: password
# we need output private ip the step "2. Create EC2 for web application" for AWX projects!
rapadura-private_ip = "10.10.0.46"
```

#### 4. Create RDS: database wordpress
```make
# set your credentials to aws in the .env file
AWS_ACCESS_KEY_ID=your_key_here
AWS_SECRET_ACCESS_KEY=your_secret_key_here
# Run terraform init to download all necessary plugins
make terraform-init
# Exec a terraform plan and puts it on a file called plano
make terraform-plan
# Uses plano to apply the changes on AWS.
make terraform-apply
# Destroy all resources created by the terraform file in this repo.
make terraform-destroy
# we need output rds for wordpress: 
rds_hostname = "database-rapadura.cakojermwtlb.us-west-1.rds.amazonaws.com"
rsd_password = "metal.corp123"
rds_port = 3306
rds_username = "databaseteste"
```

#### 5. And after running awx projects accessing websites:
- [Home](ec2-54-67-82-124.us-west-1.compute.amazonaws.com)
- [PHP](ec2-54-67-82-124.us-west-1.compute.amazonaws.com/php)
- [Apache](ec2-54-67-82-124.us-west-1.compute.amazonaws.com/apache)
- [Wordpress](ec2-54-67-82-124.us-west-1.compute.amazonaws.com/wordpress)
