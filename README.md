# AWS VPC Terraform Module 

A Terraform module which allows requesting and management of certificates from Amazon Certificate Manager.

This type of resource is supported :
- [VPC - aws_vpc](https://www.terraform.io/docs/providers/aws/r/acm_certificate.html)
- [SUBNET - aws_subnet](https://www.terraform.io/docs/providers/aws/r/subnet.html)
- [ELASTIC IP - aws_eip](https://www.terraform.io/docs/providers/aws/r/eip.html)
- [NAT GATEWAY - aws_nat_gateway](https://www.terraform.io/docs/providers/aws/r/nat_gateway.html)
- [INTERNET GATEWAY - aws_internet_gateway](https://www.terraform.io/docs/providers/aws/r/internet_gateway.html)
- [ROUTE TABLE - aws_route_table](https://www.terraform.io/docs/providers/aws/r/route_table.html)
- [ROUTE TABLE ASSOCIATION - aws_route_table_association](https://www.terraform.io/docs/providers/aws/r/route_table_association.html)
- [ROUTE - aws_route](https://www.terraform.io/docs/providers/aws/r/route.html)

# Features

The goal of this module is to give a standard way of creating and managing VPC with subnets, nat and internet gateway and finally route tables.

The module supports :

- VPC
- VPC DNS Hostnames
- VPC DNS Support
- Public Subnets
- VPC Subnet Map Public Ip on Launch
- Private Subnets 
- Internet Gateway
- Single NAT Gateway 
- NAT Gateway per AZ
- Availability Zones
- Tags

## Terraform versions

Support of Terraform 0.12 is not yet implemented. (WIP)

If you are using Terraform 0.11 you can use versions `v1.*`.

## Usage

VPC with Internet Gateway and only one NAT Gateway: 

```hcl
module "aws_vpc" {
  source                        = "app.terraform.io/<ORG_NAME>/vpc/aws"
  name                          = "test"
  azs                           = ["eu-west-1a", "eu-west-1b", "eu-west-1c"]
  internet_gateway              = "true"
  single_nat_gateway            = "true"
  vpc_cidr_block                = "10.0.0.0/16"
  vpc_public_subnet_cidr_block  = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  vpc_private_subnet_cidr_block = ["10.0.10.0/24", "10.0.11.0/24", "10.0.12.0/24"]
}
```

VPC with Internet Gateway and one NAT Gateway per Availability Zone: 

```hcl
module "aws_vpc" {
  source                        = "app.terraform.io/<ORG_NAME>/vpc/aws"
  name                          = "test"
  azs                           = ["eu-west-1a", "eu-west-1b", "eu-west-1c"]
  internet_gateway              = "true"
  single_nat_gateway            = "false"
  one_nat_gateway_per_az        = "true"
  vpc_cidr_block                = "10.0.0.0/16"
  vpc_public_subnet_cidr_block  = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  vpc_private_subnet_cidr_block = ["10.0.10.0/24", "10.0.11.0/24", "10.0.12.0/24"]
}
```

## Authors

* **Nicolas Ehrman** - *Initial work* - [Hashicorp](https://www.hashicorp.com)



