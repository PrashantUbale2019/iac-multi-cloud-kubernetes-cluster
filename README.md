# iac-multi-cloud-kubernetes-cluster
Multi-Cloud Deployment -  Deploy Federated Multi-Cloud Kubernetes Clusters on AWS and Azure

## Prerequisites

Terraform 0.14+ installed locally

an AWS account with credentials configured for Terraform

the AWS CLI

an Azure account

the Azure CLI

kubectl


### terraform init
Initializing modules...
Initializing provider plugins found in the configuration...
- Reusing previous version of hashicorp/random from the dependency lock file
- Reusing previous version of hashicorp/kubernetes from the dependency lock file
- Reusing previous version of hashicorp/tls from the dependency lock file
- Reusing previous version of hashicorp/time from the dependency lock file
- Reusing previous version of hashicorp/cloudinit from the dependency lock file
- Reusing previous version of hashicorp/aws from the dependency lock file
- Using previously-installed hashicorp/aws v5.6.2
- Using previously-installed hashicorp/random v3.9.0
- Using previously-installed hashicorp/kubernetes v3.2.1
- Using previously-installed hashicorp/tls v4.3.0
- Using previously-installed hashicorp/time v0.14.0
- Using previously-installed hashicorp/cloudinit v2.4.0

Initializing the backend...



Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
### terraform plan

Error: Unsupported Terraform Core version
│ 
│   on main.tf line 8, in terraform:
│    8:   required_version = "~> 0.14"
│ 
Fix:
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.6.2"
    }
  }
  required_version = "~> 1.0"
}


 + version                   = "1.27"

      + encryption_config {
          + resources = [
              + "secrets",
            ]

          + provider {
              + key_arn = (known after apply)
            }
        }

      + kubernetes_network_config {
          + ip_family         = (known after apply)
          + service_ipv4_cidr = (known after apply)
          + service_ipv6_cidr = (known after apply)
        }

      + timeouts {}

      + vpc_config {
          + cluster_security_group_id = (known after apply)
          + endpoint_private_access   = true
          + endpoint_public_access    = true
          + public_access_cidrs       = [
              + "0.0.0.0/0",
            ]
          + security_group_ids        = (known after apply)
          + subnet_ids                = (known after apply)
          + vpc_id                    = (known after apply)
        }
    }

  # module.eks.aws_iam_openid_connect_provider.oidc_provider[0] will be created
  + resource "aws_iam_openid_connect_provider" "oidc_provider" {
      + arn             = (known after apply)
      + client_id_list  = [
          + "sts.amazonaws.com",
        ]
      + id              = (known after apply)
      + tags            = (known after apply)
      + tags_all        = (known after apply)
      + thumbprint_list = (known after apply)
      + url             = (known after apply)
    }

  # module.eks.aws_iam_policy.cluster_encryption[0] will be created
  + resource "aws_iam_policy" "cluster_encryption" {
      + arn         = (known after apply)
      + description = "Cluster encryption policy to allow cluster role to utilize CMK provided"
      + id          = (known after apply)
      + name        = (known after apply)
      + name_prefix = (known after apply)
      + path        = "/"
      + policy      = (known after apply)
      + policy_id   = (known after apply)
      + tags_all    = (known after apply)
    }

  # module.eks.aws_iam_role.this[0] will be created
  + resource "aws_iam_role" "this" {
      + arn                   = (known after apply)
      + assume_role_policy    = jsonencode(
            {
              + Statement = [
                  + {
                      + Action    = "sts:AssumeRole"
                      + Effect    = "Allow"
                      + Principal = {
                          + Service = "eks.amazonaws.com"
                        }
                      + Sid       = "EKSClusterAssumeRole"
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + create_date           = (known after apply)
      + force_detach_policies = true
      + id                    = (known after apply)
      + managed_policy_arns   = (known after apply)
      + max_session_duration  = 3600
      + name                  = (known after apply)
      + name_prefix           = (known after apply)
      + path                  = "/"
      + tags_all              = (known after apply)
      + unique_id             = (known after apply)

      + inline_policy {
          + name   = (known after apply)
          + policy = jsonencode(
                {
                  + Statement = [
                      + {
                          + Action   = [
                              + "logs:CreateLogGroup",
                            ]
                          + Effect   = "Deny"
                          + Resource = "*"
                        },
                    ]
                  + Version   = "2012-10-17"
                }
            )
        }
    }

  # module.eks.aws_iam_role_policy_attachment.cluster_encryption[0] will be created
  + resource "aws_iam_role_policy_attachment" "cluster_encryption" {
      + id         = (known after apply)
      + policy_arn = (known after apply)
      + role       = (known after apply)
    }

  # module.eks.aws_iam_role_policy_attachment.this["AmazonEKSClusterPolicy"] will be created
  + resource "aws_iam_role_policy_attachment" "this" {
      + id         = (known after apply)
      + policy_arn = "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
      + role       = (known after apply)
    }

  # module.eks.aws_iam_role_policy_attachment.this["AmazonEKSVPCResourceController"] will be created
  + resource "aws_iam_role_policy_attachment" "this" {
      + id         = (known after apply)
      + policy_arn = "arn:aws:iam::aws:policy/AmazonEKSVPCResourceController"
      + role       = (known after apply)
    }

  # module.eks.aws_security_group.cluster[0] will be created
  + resource "aws_security_group" "cluster" {
      + arn                    = (known after apply)
      + description            = "EKS cluster security group"
      + egress                 = (known after apply)
      + id                     = (known after apply)
      + ingress                = (known after apply)
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags                   = (known after apply)
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.eks.aws_security_group.node[0] will be created
  + resource "aws_security_group" "node" {
      + arn                    = (known after apply)
      + description            = "EKS node shared security group"
      + egress                 = (known after apply)
      + id                     = (known after apply)
      + ingress                = (known after apply)
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags                   = (known after apply)
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.eks.aws_security_group_rule.cluster["ingress_nodes_443"] will be created
  + resource "aws_security_group_rule" "cluster" {
      + description              = "Node groups to cluster API"
      + from_port                = 443
      + id                       = (known after apply)
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 443
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["egress_all"] will be created
  + resource "aws_security_group_rule" "node" {
      + cidr_blocks              = [
          + "0.0.0.0/0",
        ]
      + description              = "Node all egress"
      + from_port                = 0
      + id                       = (known after apply)
      + ipv6_cidr_blocks         = [
          + "::/0",
        ]
      + prefix_list_ids          = []
      + protocol                 = "-1"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 0
      + type                     = "egress"
    }

  # module.eks.aws_security_group_rule.node["ingress_cluster_443"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Cluster API to node groups"
      + from_port                = 443
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 443
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["ingress_cluster_4443_webhook"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Cluster API to node 4443/tcp webhook"
      + from_port                = 4443
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 4443
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["ingress_cluster_6443_webhook"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Cluster API to node 6443/tcp webhook"
      + from_port                = 6443
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 6443
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["ingress_cluster_8443_webhook"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Cluster API to node 8443/tcp webhook"
      + from_port                = 8443
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 8443
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["ingress_cluster_9443_webhook"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Cluster API to node 9443/tcp webhook"
      + from_port                = 9443
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 9443
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["ingress_cluster_all"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Cluster to node all ports/protocols"
      + from_port                = 0
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "-1"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 0
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["ingress_cluster_kubelet"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Cluster API to node kubelets"
      + from_port                = 10250
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 10250
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["ingress_nodes_ephemeral"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Node to node ingress on ephemeral ports"
      + from_port                = 1025
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = true
      + source_security_group_id = (known after apply)
      + to_port                  = 65535
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["ingress_self_all"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Node to node all ports/protocols"
      + from_port                = 0
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "-1"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = true
      + source_security_group_id = (known after apply)
      + to_port                  = 0
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["ingress_self_coredns_tcp"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Node to node CoreDNS"
      + from_port                = 53
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = true
      + source_security_group_id = (known after apply)
      + to_port                  = 53
      + type                     = "ingress"
    }

  # module.eks.aws_security_group_rule.node["ingress_self_coredns_udp"] will be created
  + resource "aws_security_group_rule" "node" {
      + description              = "Node to node CoreDNS UDP"
      + from_port                = 53
      + id                       = (known after apply)
      + prefix_list_ids          = []
      + protocol                 = "udp"
      + security_group_id        = (known after apply)
      + security_group_rule_id   = (known after apply)
      + self                     = true
      + source_security_group_id = (known after apply)
      + to_port                  = 53
      + type                     = "ingress"
    }

  # module.eks.time_sleep.this[0] will be created
  + resource "time_sleep" "this" {
      + create_duration = "30s"
      + id              = (known after apply)
      + triggers        = {
          + "cluster_certificate_authority_data" = (known after apply)
          + "cluster_endpoint"                   = (known after apply)
          + "cluster_name"                       = (known after apply)
          + "cluster_version"                    = "1.27"
        }
    }

  # module.irsa-ebs-csi.data.aws_iam_policy_document.assume_role_with_oidc[0] will be read during apply
  # (config refers to values not yet known)
 <= data "aws_iam_policy_document" "assume_role_with_oidc" {
      + id   = (known after apply)
      + json = (known after apply)

      + statement (known after apply)
    }

  # module.irsa-ebs-csi.aws_iam_role.this[0] will be created
  + resource "aws_iam_role" "this" {
      + arn                   = (known after apply)
      + assume_role_policy    = (known after apply)
      + create_date           = (known after apply)
      + force_detach_policies = false
      + id                    = (known after apply)
      + managed_policy_arns   = (known after apply)
      + max_session_duration  = 3600
      + name                  = (known after apply)
      + name_prefix           = (known after apply)
      + path                  = "/"
      + tags_all              = (known after apply)
      + unique_id             = (known after apply)
        # (2 unchanged attributes hidden)

      + inline_policy (known after apply)
    }

  # module.irsa-ebs-csi.aws_iam_role_policy_attachment.custom[0] will be created
  + resource "aws_iam_role_policy_attachment" "custom" {
      + id         = (known after apply)
      + policy_arn = "arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy"
      + role       = (known after apply)
    }

  # module.vpc.aws_default_network_acl.this[0] will be created
  + resource "aws_default_network_acl" "this" {
      + arn                    = (known after apply)
      + default_network_acl_id = (known after apply)
      + id                     = (known after apply)
      + owner_id               = (known after apply)
      + tags                   = (known after apply)
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)

      + egress {
          + action          = "allow"
          + from_port       = 0
          + ipv6_cidr_block = "::/0"
          + protocol        = "-1"
          + rule_no         = 101
          + to_port         = 0
            # (1 unchanged attribute hidden)
        }
      + egress {
          + action          = "allow"
          + cidr_block      = "0.0.0.0/0"
          + from_port       = 0
          + protocol        = "-1"
          + rule_no         = 100
          + to_port         = 0
            # (1 unchanged attribute hidden)
        }

      + ingress {
          + action          = "allow"
          + from_port       = 0
          + ipv6_cidr_block = "::/0"
          + protocol        = "-1"
          + rule_no         = 101
          + to_port         = 0
            # (1 unchanged attribute hidden)
        }
      + ingress {
          + action          = "allow"
          + cidr_block      = "0.0.0.0/0"
          + from_port       = 0
          + protocol        = "-1"
          + rule_no         = 100
          + to_port         = 0
            # (1 unchanged attribute hidden)
        }
    }

  # module.vpc.aws_default_route_table.default[0] will be created
  + resource "aws_default_route_table" "default" {
      + arn                    = (known after apply)
      + default_route_table_id = (known after apply)
      + id                     = (known after apply)
      + owner_id               = (known after apply)
      + route                  = (known after apply)
      + tags                   = (known after apply)
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)

      + timeouts {
          + create = "5m"
          + update = "5m"
        }
    }

  # module.vpc.aws_default_security_group.this[0] will be created
  + resource "aws_default_security_group" "this" {
      + arn                    = (known after apply)
      + description            = (known after apply)
      + egress                 = (known after apply)
      + id                     = (known after apply)
      + ingress                = (known after apply)
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags                   = (known after apply)
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.vpc.aws_eip.nat[0] will be created
  + resource "aws_eip" "nat" {
      + allocation_id        = (known after apply)
      + association_id       = (known after apply)
      + carrier_ip           = (known after apply)
      + customer_owned_ip    = (known after apply)
      + domain               = "vpc"
      + id                   = (known after apply)
      + instance             = (known after apply)
      + network_border_group = (known after apply)
      + network_interface    = (known after apply)
      + private_dns          = (known after apply)
      + private_ip           = (known after apply)
      + public_dns           = (known after apply)
      + public_ip            = (known after apply)
      + public_ipv4_pool     = (known after apply)
      + tags                 = (known after apply)
      + tags_all             = (known after apply)
      + vpc                  = (known after apply)
    }

  # module.vpc.aws_internet_gateway.this[0] will be created
  + resource "aws_internet_gateway" "this" {
      + arn      = (known after apply)
      + id       = (known after apply)
      + owner_id = (known after apply)
      + tags     = (known after apply)
      + tags_all = (known after apply)
      + vpc_id   = (known after apply)
    }

  # module.vpc.aws_nat_gateway.this[0] will be created
  + resource "aws_nat_gateway" "this" {
      + allocation_id        = (known after apply)
      + association_id       = (known after apply)
      + connectivity_type    = "public"
      + id                   = (known after apply)
      + network_interface_id = (known after apply)
      + private_ip           = (known after apply)
      + public_ip            = (known after apply)
      + subnet_id            = (known after apply)
      + tags                 = (known after apply)
      + tags_all             = (known after apply)
    }

  # module.vpc.aws_route.private_nat_gateway[0] will be created
  + resource "aws_route" "private_nat_gateway" {
      + destination_cidr_block = "0.0.0.0/0"
      + id                     = (known after apply)
      + instance_id            = (known after apply)
      + instance_owner_id      = (known after apply)
      + nat_gateway_id         = (known after apply)
      + network_interface_id   = (known after apply)
      + origin                 = (known after apply)
      + route_table_id         = (known after apply)
      + state                  = (known after apply)

      + timeouts {
          + create = "5m"
        }
    }

  # module.vpc.aws_route.public_internet_gateway[0] will be created
  + resource "aws_route" "public_internet_gateway" {
      + destination_cidr_block = "0.0.0.0/0"
      + gateway_id             = (known after apply)
      + id                     = (known after apply)
      + instance_id            = (known after apply)
      + instance_owner_id      = (known after apply)
      + network_interface_id   = (known after apply)
      + origin                 = (known after apply)
      + route_table_id         = (known after apply)
      + state                  = (known after apply)

      + timeouts {
          + create = "5m"
        }
    }

  # module.vpc.aws_route_table.private[0] will be created
  + resource "aws_route_table" "private" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = (known after apply)
      + tags             = (known after apply)
      + tags_all         = (known after apply)
      + vpc_id           = (known after apply)
    }

  # module.vpc.aws_route_table.public[0] will be created
  + resource "aws_route_table" "public" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = (known after apply)
      + tags             = (known after apply)
      + tags_all         = (known after apply)
      + vpc_id           = (known after apply)
    }

  # module.vpc.aws_route_table_association.private[0] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.vpc.aws_route_table_association.private[1] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.vpc.aws_route_table_association.private[2] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.vpc.aws_route_table_association.public[0] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.vpc.aws_route_table_association.public[1] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.vpc.aws_route_table_association.public[2] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.vpc.aws_subnet.private[0] will be created
  + resource "aws_subnet" "private" {
      + arn                                            = (known after apply)
      + assign_ipv6_address_on_creation                = false
      + availability_zone                              = "us-east-2a"
      + availability_zone_id                           = (known after apply)
      + cidr_block                                     = "10.0.1.0/24"
      + enable_dns64                                   = false
      + enable_resource_name_dns_a_record_on_launch    = false
      + enable_resource_name_dns_aaaa_record_on_launch = false
      + id                                             = (known after apply)
      + ipv6_cidr_block_association_id                 = (known after apply)
      + ipv6_native                                    = false
      + map_public_ip_on_launch                        = false
      + owner_id                                       = (known after apply)
      + private_dns_hostname_type_on_launch            = (known after apply)
      + tags                                           = (known after apply)
      + tags_all                                       = (known after apply)
      + vpc_id                                         = (known after apply)
    }

  # module.vpc.aws_subnet.private[1] will be created
  + resource "aws_subnet" "private" {
      + arn                                            = (known after apply)
      + assign_ipv6_address_on_creation                = false
      + availability_zone                              = "us-east-2b"
      + availability_zone_id                           = (known after apply)
      + cidr_block                                     = "10.0.2.0/24"
      + enable_dns64                                   = false
      + enable_resource_name_dns_a_record_on_launch    = false
      + enable_resource_name_dns_aaaa_record_on_launch = false
      + id                                             = (known after apply)
      + ipv6_cidr_block_association_id                 = (known after apply)
      + ipv6_native                                    = false
      + map_public_ip_on_launch                        = false
      + owner_id                                       = (known after apply)
      + private_dns_hostname_type_on_launch            = (known after apply)
      + tags                                           = (known after apply)
      + tags_all                                       = (known after apply)
      + vpc_id                                         = (known after apply)
    }

  # module.vpc.aws_subnet.private[2] will be created
  + resource "aws_subnet" "private" {
      + arn                                            = (known after apply)
      + assign_ipv6_address_on_creation                = false
      + availability_zone                              = "us-east-2c"
      + availability_zone_id                           = (known after apply)
      + cidr_block                                     = "10.0.3.0/24"
      + enable_dns64                                   = false
      + enable_resource_name_dns_a_record_on_launch    = false
      + enable_resource_name_dns_aaaa_record_on_launch = false
      + id                                             = (known after apply)
      + ipv6_cidr_block_association_id                 = (known after apply)
      + ipv6_native                                    = false
      + map_public_ip_on_launch                        = false
      + owner_id                                       = (known after apply)
      + private_dns_hostname_type_on_launch            = (known after apply)
      + tags                                           = (known after apply)
      + tags_all                                       = (known after apply)
      + vpc_id                                         = (known after apply)
    }

  # module.vpc.aws_subnet.public[0] will be created
  + resource "aws_subnet" "public" {
      + arn                                            = (known after apply)
      + assign_ipv6_address_on_creation                = false
      + availability_zone                              = "us-east-2a"
      + availability_zone_id                           = (known after apply)
      + cidr_block                                     = "10.0.4.0/24"
      + enable_dns64                                   = false
      + enable_resource_name_dns_a_record_on_launch    = false
      + enable_resource_name_dns_aaaa_record_on_launch = false
      + id                                             = (known after apply)
      + ipv6_cidr_block_association_id                 = (known after apply)
      + ipv6_native                                    = false
      + map_public_ip_on_launch                        = false
      + owner_id                                       = (known after apply)
      + private_dns_hostname_type_on_launch            = (known after apply)
      + tags                                           = (known after apply)
      + tags_all                                       = (known after apply)
      + vpc_id                                         = (known after apply)
    }

  # module.vpc.aws_subnet.public[1] will be created
  + resource "aws_subnet" "public" {
      + arn                                            = (known after apply)
      + assign_ipv6_address_on_creation                = false
      + availability_zone                              = "us-east-2b"
      + availability_zone_id                           = (known after apply)
      + cidr_block                                     = "10.0.5.0/24"
      + enable_dns64                                   = false
      + enable_resource_name_dns_a_record_on_launch    = false
      + enable_resource_name_dns_aaaa_record_on_launch = false
      + id                                             = (known after apply)
      + ipv6_cidr_block_association_id                 = (known after apply)
      + ipv6_native                                    = false
      + map_public_ip_on_launch                        = false
      + owner_id                                       = (known after apply)
      + private_dns_hostname_type_on_launch            = (known after apply)
      + tags                                           = (known after apply)
      + tags_all                                       = (known after apply)
      + vpc_id                                         = (known after apply)
    }

  # module.vpc.aws_subnet.public[2] will be created
  + resource "aws_subnet" "public" {
      + arn                                            = (known after apply)
      + assign_ipv6_address_on_creation                = false
      + availability_zone                              = "us-east-2c"
      + availability_zone_id                           = (known after apply)
      + cidr_block                                     = "10.0.6.0/24"
      + enable_dns64                                   = false
      + enable_resource_name_dns_a_record_on_launch    = false
      + enable_resource_name_dns_aaaa_record_on_launch = false
      + id                                             = (known after apply)
      + ipv6_cidr_block_association_id                 = (known after apply)
      + ipv6_native                                    = false
      + map_public_ip_on_launch                        = false
      + owner_id                                       = (known after apply)
      + private_dns_hostname_type_on_launch            = (known after apply)
      + tags                                           = (known after apply)
      + tags_all                                       = (known after apply)
      + vpc_id                                         = (known after apply)
    }

  # module.vpc.aws_vpc.this[0] will be created
  + resource "aws_vpc" "this" {
      + arn                                  = (known after apply)
      + cidr_block                           = "10.0.0.0/16"
      + default_network_acl_id               = (known after apply)
      + default_route_table_id               = (known after apply)
      + default_security_group_id            = (known after apply)
      + dhcp_options_id                      = (known after apply)
      + enable_dns_hostnames                 = true
      + enable_dns_support                   = true
      + enable_network_address_usage_metrics = (known after apply)
      + id                                   = (known after apply)
      + instance_tenancy                     = "default"
      + ipv6_association_id                  = (known after apply)
      + ipv6_cidr_block                      = (known after apply)
      + ipv6_cidr_block_network_border_group = (known after apply)
      + main_route_table_id                  = (known after apply)
      + owner_id                             = (known after apply)
      + tags                                 = (known after apply)
      + tags_all                             = (known after apply)
    }

  # module.eks.module.eks_managed_node_group["consul"].aws_eks_node_group.this[0] will be created
  + resource "aws_eks_node_group" "this" {
      + ami_type               = "AL2_x86_64"
      + arn                    = (known after apply)
      + capacity_type          = (known after apply)
      + cluster_name           = (known after apply)
      + disk_size              = (known after apply)
      + id                     = (known after apply)
      + instance_types         = [
          + "t3a.medium",
        ]
      + node_group_name        = (known after apply)
      + node_group_name_prefix = "consul-group-"
      + node_role_arn          = (known after apply)
      + release_version        = (known after apply)
      + resources              = (known after apply)
      + status                 = (known after apply)
      + subnet_ids             = (known after apply)
      + tags                   = {
          + "Name" = "consul-group"
        }
      + tags_all               = {
          + "Name" = "consul-group"
        }
      + version                = "1.27"

      + launch_template {
          + id      = (known after apply)
          + name    = (known after apply)
          + version = (known after apply)
        }

      + scaling_config {
          + desired_size = 3
          + max_size     = 3
          + min_size     = 1
        }

      + timeouts {}

      + update_config {
          + max_unavailable_percentage = 33
        }
    }

  # module.eks.module.eks_managed_node_group["consul"].aws_iam_role.this[0] will be created
  + resource "aws_iam_role" "this" {
      + arn                   = (known after apply)
      + assume_role_policy    = jsonencode(
            {
              + Statement = [
                  + {
                      + Action    = "sts:AssumeRole"
                      + Effect    = "Allow"
                      + Principal = {
                          + Service = "ec2.amazonaws.com"
                        }
                      + Sid       = "EKSNodeAssumeRole"
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + create_date           = (known after apply)
      + description           = "EKS managed node group IAM role"
      + force_detach_policies = true
      + id                    = (known after apply)
      + managed_policy_arns   = (known after apply)
      + max_session_duration  = 3600
      + name                  = (known after apply)
      + name_prefix           = "consul-group-eks-node-group-"
      + path                  = "/"
      + tags_all              = (known after apply)
      + unique_id             = (known after apply)

      + inline_policy (known after apply)
    }

  # module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly"] will be created
  + resource "aws_iam_role_policy_attachment" "this" {
      + id         = (known after apply)
      + policy_arn = "arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly"
      + role       = (known after apply)
    }

  # module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy"] will be created
  + resource "aws_iam_role_policy_attachment" "this" {
      + id         = (known after apply)
      + policy_arn = "arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy"
      + role       = (known after apply)
    }

  # module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy"] will be created
  + resource "aws_iam_role_policy_attachment" "this" {
      + id         = (known after apply)
      + policy_arn = "arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy"
      + role       = (known after apply)
    }

  # module.eks.module.eks_managed_node_group["consul"].aws_launch_template.this[0] will be created
  + resource "aws_launch_template" "this" {
      + arn                    = (known after apply)
      + default_version        = (known after apply)
      + description            = "Custom launch template for consul-group EKS managed node group"
      + id                     = (known after apply)
      + latest_version         = (known after apply)
      + name                   = (known after apply)
      + name_prefix            = "consul-"
      + tags_all               = (known after apply)
      + update_default_version = true
      + vpc_security_group_ids = (known after apply)
        # (2 unchanged attributes hidden)

      + metadata_options {
          + http_endpoint               = "enabled"
          + http_protocol_ipv6          = (known after apply)
          + http_put_response_hop_limit = 2
          + http_tokens                 = "required"
          + instance_metadata_tags      = (known after apply)
        }

      + monitoring {
          + enabled = true
        }

      + tag_specifications {
          + resource_type = "instance"
          + tags          = {
              + "Name" = "consul-group"
            }
        }
      + tag_specifications {
          + resource_type = "network-interface"
          + tags          = {
              + "Name" = "consul-group"
            }
        }
      + tag_specifications {
          + resource_type = "volume"
          + tags          = {
              + "Name" = "consul-group"
            }
        }
    }

  # module.eks.module.kms.data.aws_iam_policy_document.this[0] will be read during apply
  # (config refers to values not yet known)
 <= data "aws_iam_policy_document" "this" {
      + id                        = (known after apply)
      + json                      = (known after apply)
      + override_policy_documents = []
      + source_policy_documents   = []

      + statement {
          + actions   = [
              + "kms:CancelKeyDeletion",
              + "kms:Create*",
              + "kms:Delete*",
              + "kms:Describe*",
              + "kms:Disable*",
              + "kms:Enable*",
              + "kms:Get*",
              + "kms:List*",
              + "kms:Put*",
              + "kms:Revoke*",
              + "kms:ScheduleKeyDeletion",
              + "kms:TagResource",
              + "kms:UntagResource",
              + "kms:Update*",
            ]
          + resources = [
              + "*",
            ]
          + sid       = "KeyAdministration"

          + principals {
              + identifiers = [
                  + "arn:aws:iam::[aws-id]:user/iac-terraform-aws",
                ]
              + type        = "AWS"
            }
        }
      + statement {
          + actions   = [
              + "kms:Decrypt",
              + "kms:DescribeKey",
              + "kms:Encrypt",
              + "kms:GenerateDataKey*",
              + "kms:ReEncrypt*",
            ]
          + resources = [
              + "*",
            ]
          + sid       = "KeyUsage"

          + principals {
              + identifiers = [
                  + (known after apply),
                ]
              + type        = "AWS"
            }
        }
    }

  # module.eks.module.kms.aws_kms_alias.this["cluster"] will be created
  + resource "aws_kms_alias" "this" {
      + arn            = (known after apply)
      + id             = (known after apply)
      + name           = (known after apply)
      + name_prefix    = (known after apply)
      + target_key_arn = (known after apply)
      + target_key_id  = (known after apply)
    }

  # module.eks.module.kms.aws_kms_key.this[0] will be created
  + resource "aws_kms_key" "this" {
      + arn                                = (known after apply)
      + bypass_policy_lockout_safety_check = false
      + customer_master_key_spec           = "SYMMETRIC_DEFAULT"
      + description                        = (known after apply)
      + enable_key_rotation                = true
      + id                                 = (known after apply)
      + is_enabled                         = true
      + key_id                             = (known after apply)
      + key_usage                          = "ENCRYPT_DECRYPT"
      + multi_region                       = false
      + policy                             = (known after apply)
      + tags_all                           = (known after apply)
    }

Plan: 59 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + cluster_id   = (known after apply)
  + cluster_name = (known after apply)
  + region       = "us-east-2"
╷
│ Warning: Deprecated Resource
│ 
│   with module.eks.kubernetes_config_map.aws_auth,
│   on .terraform/modules/eks/main.tf line 536, in resource "kubernetes_config_map" "aws_auth":
│  536: resource "kubernetes_config_map" "aws_auth" {
│ 
│ Deprecated; use kubernetes_config_map_v1.

## terraform apply
Warning: Deprecated Resource
│ 
│   with module.eks.kubernetes_config_map.aws_auth,
│   on .terraform/modules/eks/main.tf line 536, in resource "kubernetes_config_map" "aws_auth":
│  536: resource "kubernetes_config_map" "aws_auth" {
│ 
│ Deprecated; use kubernetes_config_map_v1.
╵
╷Error: fetching Availability Zones: UnauthorizedOperation: You are not authorized to perform this operation. User: arn:aws:iam::[aws-id]:user/iac-terraform-aws is not authorized to perform: ec2:DescribeAvailabilityZones because no identity-based policy allows the ec2:DescribeAvailabilityZones action
│       status code: 403, request id: a1844c89-3015-49cb-b6fd-00eebd61c594
│ 
│   with data.aws_availability_zones.available,
│   on main.tf line 15, in data "aws_availability_zones" "available":
│   15: data "aws_availability_zones" "available" {}

Fix :

Option 1: Attach an Inline Policy (Recommended for least privilege)
If you want to grant only the missing permission, attach this inline JSON policy to the IAM user iac-terraform-aws:
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ec2:DescribeAvailabilityZones",
            "Resource": "*"
        }
    ]
}
Option 2: Attach an AWS Managed Policy
If this IAM user is intended to manage a wider range of network infrastructure, you can attach the AWS-managed policy:

AmazonEC2ReadOnlyAccess (Allows describing AZs, VPCs, subnets, instances, etc.)

Steps to Apply in AWS Console
Open the IAM Console.

Click on Users in the left sidebar and select iac-terraform-aws.

Under the Permissions tab, click Add permissions -> Create inline policy (or Attach policies directly if using Option 2).

If creating an inline policy, switch to the JSON tab, paste the JSON snippet from above, and save it.

│ Error: creating CloudWatch Logs Log Group (/aws/eks/education-eks-XZbJw1Cj/cluster): AccessDeniedException: User: arn:aws:iam::[aws-id]:user/iac-terraform-aws is not authorized to perform: logs:CreateLogGroup on resource: arn:aws:logs:us-east-2:[aws-id]:log-group:/aws/eks/education-eks-XZbJw1Cj/cluster:log-stream: because no identity-based policy allows the logs:CreateLogGroup action
│       status code: 400, request id: 041d475d-4f16-4761-90ef-9d292500094d
│ 
│   with module.eks.aws_cloudwatch_log_group.this[0],
│   on .terraform/modules/eks/main.tf line 106, in resource "aws_cloudwatch_log_group" "this":
│  106: resource "aws_cloudwatch_log_group" "this" {
│ 
╵
╷
│ Error: creating IAM Role (education-eks-XZbJw1Cj-cluster-20260709071307422800000002): AccessDenied: User: arn:aws:iam::[aws-id]:user/iac-terraform-aws is not authorized to perform: iam:CreateRole on resource: arn:aws:iam::[aws-id]:role/education-eks-XZbJw1Cj-cluster-20260709071307422800000002 because no identity-based policy allows the iam:CreateRole action
│       status code: 403, request id: 7e094351-09bf-4101-a477-89c4c45089e1
│ 
│   with module.eks.aws_iam_role.this[0],
│   on .terraform/modules/eks/main.tf line 285, in resource "aws_iam_role" "this":
│  285: resource "aws_iam_role" "this" {
│ 
╵
╷
│ Error: creating EC2 VPC: UnauthorizedOperation: You are not authorized to perform this operation. User: arn:aws:iam::[aws-id]:user/iac-terraform-aws is not authorized to perform: ec2:CreateVpc on resource: arn:aws:ec2:us-east-2:[aws-id]:vpc/* because no identity-based policy allows the ec2:CreateVpc action. Encoded authorization failure message: 
│       status code: 403, request id: 1f4c5399-6962-435e-abed-21ecb945806e
│ 
│   with module.vpc.aws_vpc.this[0],
│   on .terraform/modules/vpc/main.tf line 29, in resource "aws_vpc" "this":
│   29: resource "aws_vpc" "this" {
│ 
╵
╷
│ Error: creating IAM Role (consul-group-eks-node-group-20260709071307422400000001): AccessDenied: User: arn:aws:iam::[aws-id]:user/iac-terraform-aws is not authorized to perform: iam:CreateRole on resource: arn:aws:iam::[aws-id]:role/consul-group-eks-node-group-20260709071307422400000001 because no identity-based policy allows the iam:CreateRole action
│       status code: 403, request id: d20fc310-c117-4bfe-ba51-02f47b8385f5
│ 
│   with module.eks.module.eks_managed_node_group["consul"].aws_iam_role.this[0],
│   on .terraform/modules/eks/modules/eks-managed-node-group/main.tf line 417, in resource "aws_iam_role" "this":
│  417: resource "aws_iam_role" "this" {
│ 
### Resolution : 
Option 1. Attach AdministratorAccess (Recommended for Sandbox/Learning)
If this is an isolated learning or test account, the cleanest solution is to give the user full admin rights.

Open the AWS IAM Console.
Go to Users -> iac-terraform-aws.
Under Permissions, click Add permissions -> Attach policies directly.
Search for and check AdministratorAccess.
Save changes.

Option 2. 
Attach an Inline Policy (Least Privilege)
To grant only the specific CloudWatch Logs permissions required to manage this log group (and any future ones Terraform creates), attach this inline JSON policy to your IAM user iac-terraform-aws


### remove terraform.tfstate and lock.hcl files and run terraform init, plan, apply
random_string.suffix: Creating...
random_string.suffix: Creation complete after 0s [id=qo9I4mfc]
module.eks.aws_cloudwatch_log_group.this[0]: Creating...
module.eks.module.eks_managed_node_group["consul"].aws_iam_role.this[0]: Creating...
module.vpc.aws_vpc.this[0]: Creating...
module.eks.aws_iam_role.this[0]: Creating...
module.eks.aws_cloudwatch_log_group.this[0]: Creation complete after 2s [id=/aws/eks/iac-terraform-eks-qo9I4mfc/cluster]
module.eks.module.eks_managed_node_group["consul"].aws_iam_role.this[0]: Creation complete after 2s [id=consul-group-eks-node-group-20260709073617838600000001]
module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly"]: Creating...
module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy"]: Creating...
module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy"]: Creating...
module.eks.aws_iam_role.this[0]: Creation complete after 3s [id=iac-terraform-eks-qo9I4mfc-cluster-20260709073617839200000002]
module.eks.aws_iam_role_policy_attachment.this["AmazonEKSVPCResourceController"]: Creating...
module.eks.aws_iam_role_policy_attachment.this["AmazonEKSClusterPolicy"]: Creating...
module.eks.module.kms.data.aws_iam_policy_document.this[0]: Reading...
module.eks.module.kms.data.aws_iam_policy_document.this[0]: Read complete after 0s [id=1498183619]
module.eks.module.kms.aws_kms_key.this[0]: Creating...
module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy"]: Creation complete after 1s [id=consul-group-eks-node-group-20260709073617838600000001-20260709073620276000000003]
module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy"]: Creation complete after 1s [id=consul-group-eks-node-group-20260709073617838600000001-20260709073620632700000005]
module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly"]: Creation complete after 1s [id=consul-group-eks-node-group-20260709073617838600000001-20260709073620475100000004]
module.eks.aws_iam_role_policy_attachment.this["AmazonEKSClusterPolicy"]: Creation complete after 0s [id=iac-terraform-eks-qo9I4mfc-cluster-20260709073617839200000002-20260709073621062000000006]
module.eks.aws_iam_role_policy_attachment.this["AmazonEKSVPCResourceController"]: Creation complete after 1s [id=iac-terraform-eks-qo9I4mfc-cluster-20260709073617839200000002-20260709073621267300000007]
module.vpc.aws_vpc.this[0]: Still creating... [00m10s elapsed]
module.eks.module.kms.aws_kms_key.this[0]: Still creating... [00m10s elapsed]
module.vpc.aws_vpc.this[0]: Creation complete after 16s [id=vpc-0dcfe89c6ebf3a525]
module.vpc.aws_internet_gateway.this[0]: Creating...
module.vpc.aws_route_table.private[0]: Creating...
module.vpc.aws_subnet.private[1]: Creating...
module.vpc.aws_default_route_table.default[0]: Creating...
module.vpc.aws_subnet.private[0]: Creating...
module.eks.aws_security_group.cluster[0]: Creating...
module.vpc.aws_default_security_group.this[0]: Creating...
module.vpc.aws_subnet.public[1]: Creating...
module.vpc.aws_default_network_acl.this[0]: Creating...
module.vpc.aws_default_route_table.default[0]: Creation complete after 1s [id=rtb-047360c1b64942173]
module.eks.aws_security_group.node[0]: Creating...
module.vpc.aws_internet_gateway.this[0]: Creation complete after 2s [id=igw-017dd568a11e8825f]
module.vpc.aws_route_table.public[0]: Creating...
module.vpc.aws_route_table.private[0]: Creation complete after 2s [id=rtb-05bba14b38101a492]
module.vpc.aws_subnet.public[2]: Creating...
module.vpc.aws_subnet.private[0]: Creation complete after 2s [id=subnet-0841c3fb94a2175f3]
module.vpc.aws_subnet.public[0]: Creating...
module.vpc.aws_subnet.public[1]: Creation complete after 2s [id=subnet-0a2cafc08d37679d4]
module.vpc.aws_subnet.private[2]: Creating...
module.vpc.aws_route_table.public[0]: Creation complete after 1s [id=rtb-0797c24ffc182d88f]
module.vpc.aws_eip.nat[0]: Creating...
module.vpc.aws_subnet.public[0]: Creation complete after 1s [id=subnet-04dbf123a4e9bd0c8]
module.vpc.aws_route.public_internet_gateway[0]: Creating...
module.vpc.aws_subnet.public[2]: Creation complete after 1s [id=subnet-04b5c7bd476560aba]
module.vpc.aws_subnet.private[2]: Creation complete after 1s [id=subnet-0b798607cb45f3516]
module.vpc.aws_route_table_association.public[2]: Creating...
module.vpc.aws_route_table_association.public[1]: Creating...
module.vpc.aws_default_network_acl.this[0]: Creation complete after 4s [id=acl-05d8ebaa6e1fe9b15]
module.vpc.aws_route_table_association.public[0]: Creating...
module.vpc.aws_default_security_group.this[0]: Creation complete after 4s [id=sg-03a22c3efaccfd32d]
module.eks.aws_security_group.cluster[0]: Creation complete after 4s [id=sg-0d5ec2a2442b3b2c3]
module.vpc.aws_subnet.private[1]: Creation complete after 4s [id=subnet-089affa567e268031]
module.vpc.aws_route_table_association.private[1]: Creating...
module.vpc.aws_route_table_association.private[0]: Creating...
module.vpc.aws_route_table_association.private[2]: Creating...
module.vpc.aws_route_table_association.public[2]: Creation complete after 1s [id=rtbassoc-0289806dbc1fbd953]
module.vpc.aws_route_table_association.public[1]: Creation complete after 1s [id=rtbassoc-00921caec8b30b387]
module.vpc.aws_eip.nat[0]: Creation complete after 2s [id=eipalloc-0090bd9e11e84b42c]
module.vpc.aws_nat_gateway.this[0]: Creating...
module.vpc.aws_route_table_association.public[0]: Creation complete after 1s [id=rtbassoc-00d19b67bf10e717d]
module.vpc.aws_route.public_internet_gateway[0]: Creation complete after 2s [id=r-rtb-0797c24ffc182d88f1080289494]
module.eks.aws_security_group.node[0]: Creation complete after 4s [id=sg-0077e765d6ec26274]
module.eks.aws_security_group_rule.node["ingress_self_coredns_udp"]: Creating...
module.eks.aws_security_group_rule.node["ingress_self_all"]: Creating...
module.eks.aws_security_group_rule.node["ingress_cluster_kubelet"]: Creating...
module.eks.aws_security_group_rule.node["egress_all"]: Creating...
module.eks.aws_security_group_rule.node["ingress_cluster_9443_webhook"]: Creating...
module.vpc.aws_route_table_association.private[0]: Creation complete after 1s [id=rtbassoc-073a6c119220021b1]
module.eks.aws_security_group_rule.node["ingress_cluster_443"]: Creating...
module.vpc.aws_route_table_association.private[2]: Creation complete after 1s [id=rtbassoc-094f46bc432ece4a4]
module.vpc.aws_route_table_association.private[1]: Creation complete after 1s [id=rtbassoc-01e4e565e513cdef1]
module.eks.aws_security_group_rule.node["ingress_self_coredns_tcp"]: Creating...
module.eks.aws_security_group_rule.node["ingress_cluster_4443_webhook"]: Creating...
module.eks.aws_security_group_rule.node["egress_all"]: Creation complete after 1s [id=sgrule-1987380767]
module.eks.aws_security_group_rule.node["ingress_cluster_6443_webhook"]: Creating...
module.eks.module.kms.aws_kms_key.this[0]: Still creating... [00m20s elapsed]
module.eks.aws_security_group_rule.node["ingress_cluster_kubelet"]: Creation complete after 3s [id=sgrule-328053351]
module.eks.aws_security_group_rule.node["ingress_nodes_ephemeral"]: Creating...
module.eks.module.kms.aws_kms_key.this[0]: Creation complete after 21s [id=c090eca0-25ea-487d-93ab-1346c2b920d6]
module.eks.aws_security_group_rule.cluster["ingress_nodes_443"]: Creating...
module.eks.aws_security_group_rule.node["ingress_self_all"]: Creation complete after 4s [id=sgrule-2078336456]
module.eks.aws_security_group_rule.node["ingress_cluster_8443_webhook"]: Creating...
module.eks.aws_security_group_rule.cluster["ingress_nodes_443"]: Creation complete after 2s [id=sgrule-859140573]
module.eks.aws_security_group_rule.node["ingress_cluster_all"]: Creating...
module.eks.aws_security_group_rule.node["ingress_self_coredns_udp"]: Creation complete after 5s [id=sgrule-3465729470]
module.eks.module.kms.aws_kms_alias.this["cluster"]: Creating...
module.eks.module.kms.aws_kms_alias.this["cluster"]: Creation complete after 1s [id=alias/eks/iac-terraform-eks-qo9I4mfc]
module.eks.aws_iam_policy.cluster_encryption[0]: Creating...
module.eks.aws_security_group_rule.node["ingress_cluster_9443_webhook"]: Creation complete after 6s [id=sgrule-666380463]
module.eks.aws_iam_policy.cluster_encryption[0]: Creation complete after 1s [id=arn:aws:iam::[aws-id]:policy/iac-terraform-eks-qo9I4mfc-cluster-ClusterEncryption2026070907364470490000000b]
module.eks.aws_iam_role_policy_attachment.cluster_encryption[0]: Creating...
module.eks.aws_iam_role_policy_attachment.cluster_encryption[0]: Creation complete after 0s [id=iac-terraform-eks-qo9I4mfc-cluster-20260709073617839200000002-2026070907364601290000000c]
module.eks.aws_security_group_rule.node["ingress_cluster_443"]: Creation complete after 8s [id=sgrule-975581061]
module.eks.aws_security_group_rule.node["ingress_self_coredns_tcp"]: Creation complete after 9s [id=sgrule-1791850065]
module.vpc.aws_nat_gateway.this[0]: Still creating... [00m10s elapsed]
module.eks.aws_security_group_rule.node["ingress_cluster_4443_webhook"]: Creation complete after 10s [id=sgrule-2567389395]
module.eks.aws_security_group_rule.node["ingress_cluster_6443_webhook"]: Still creating... [00m10s elapsed]
module.eks.aws_security_group_rule.node["ingress_cluster_6443_webhook"]: Creation complete after 10s [id=sgrule-1346709317]
module.eks.aws_security_group_rule.node["ingress_nodes_ephemeral"]: Still creating... [00m10s elapsed]
module.eks.aws_security_group_rule.node["ingress_nodes_ephemeral"]: Creation complete after 10s [id=sgrule-1600333283]
module.eks.aws_security_group_rule.node["ingress_cluster_8443_webhook"]: Still creating... [00m10s elapsed]
module.eks.aws_security_group_rule.node["ingress_cluster_8443_webhook"]: Creation complete after 10s [id=sgrule-1125718884]
module.eks.aws_security_group_rule.node["ingress_cluster_all"]: Still creating... [00m10s elapsed]
module.eks.aws_security_group_rule.node["ingress_cluster_all"]: Creation complete after 10s [id=sgrule-251785042]
module.eks.aws_eks_cluster.this[0]: Creating...
.
module.vpc.aws_nat_gateway.this[0]: Still creating... [01m20s elapsed]
module.vpc.aws_nat_gateway.this[0]: Creation complete after 1m28s [id=nat-0079dd80b12cc01c5]
module.vpc.aws_route.private_nat_gateway[0]: Creating...
module.vpc.aws_route.private_nat_gateway[0]: Creation complete after 1s [id=r-rtb-05bba14b38101a4921080289494]
╷
│ Warning: Deprecated Resource
│ 
│   with module.eks.kubernetes_config_map.aws_auth,
│   on .terraform/modules/eks/main.tf line 536, in resource "kubernetes_config_map" "aws_auth":
│  536: resource "kubernetes_config_map" "aws_auth" {
│ 
│ Deprecated; use kubernetes_config_map_v1.
╵
╷
│ Error: creating EKS Cluster (iac-terraform-eks-qo9I4mfc): InvalidParameterException: unsupported Kubernetes version 1.27
│ {
│   RespMetadata: {
│     StatusCode: 400,
│     RequestID: "ec5eb295-bdb9-45a2-9c6e-fefa2413ef43"
│   },
│   ClusterName: "iac-terraform-eks-qo9I4mfc",
│   Message_: "unsupported Kubernetes version 1.27"
│ }
│ 
│   with module.eks.aws_eks_cluster.this[0],
│   on .terraform/modules/eks/main.tf line 25, in resource "aws_eks_cluster" "this":
│   25: resource "aws_eks_cluster" "this" {

│ Resolution :
Kubernetes version 1.27 has reached its End of Life (EOL) on Amazon EKS and is no longer available for creating new clusters
Locate the aws_eks_cluster resource block in your Terraform configuration in main.tf and update the version parameter to a supported release (such as 1.34 or 1.35)
cluster_version = "1.34"

run terraform destroy and remove state and lock files delete cluster created form AWS console

Warning: Deprecated Resource
│ 
│   with module.eks.kubernetes_config_map.aws_auth,
│   on .terraform/modules/eks/main.tf line 536, in resource "kubernetes_config_map" "aws_auth":
│  536: resource "kubernetes_config_map" "aws_auth" {
│ 
│ Deprecated; use kubernetes_config_map_v1.

module "eks" {
  source  = "terraform-aws-modules/eks/aws"
 version = "~> 20.0"


Resolution : terraform init -upgrade
Upgrading modules...
Downloading registry.terraform.io/terraform-aws-modules/iam/aws 4.7.0 for irsa-ebs-csi...
- irsa-ebs-csi in .terraform/modules/irsa-ebs-csi/modules/iam-assumable-role-with-oidc
Downloading registry.terraform.io/terraform-aws-modules/eks/aws 19.15.3 for eks...
- eks in .terraform/modules/eks
Downloading registry.terraform.io/terraform-aws-modules/vpc/aws 5.1.1 for vpc...
- vpc in .terraform/modules/vpc
- eks.fargate_profile in .terraform/modules/eks/modules/fargate-profile
Downloading registry.terraform.io/terraform-aws-modules/kms/aws 1.1.0 for eks.kms...
- eks.kms in .terraform/modules/eks.kms
- eks.eks_managed_node_group in .terraform/modules/eks/modules/eks-managed-node-group
- eks.self_managed_node_group in .terraform/modules/eks/modules/self-managed-node-group
- eks.eks_managed_node_group.user_data in .terraform/modules/eks/modules/_user_data
- eks.self_managed_node_group.user_data in .terraform/modules/eks/modules/_user_data
Initializing provider plugins found in the configuration...
- Finding hashicorp/time versions matching ">= 0.9.0"...
- Finding hashicorp/tls versions matching ">= 3.0.0"...
- Finding hashicorp/cloudinit versions matching ">= 2.0.0"...
- Finding hashicorp/aws versions matching ">= 2.23.0, >= 3.72.0, >= 4.47.0, >= 4.57.0, >= 5.0.0, ~> 5.6.2"...
- Finding latest version of hashicorp/random...
- Finding hashicorp/kubernetes versions matching ">= 2.10.0"...
- Using previously-installed hashicorp/random v3.9.0
- Using previously-installed hashicorp/kubernetes v3.2.1
- Using previously-installed hashicorp/time v0.14.0
- Using previously-installed hashicorp/tls v4.3.0
- Using previously-installed hashicorp/cloudinit v2.4.0
- Using previously-installed hashicorp/aws v5.6.2

Initializing the backend...

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

Error: Failed to query available provider packages
│ 
│ Could not retrieve the list of available versions for provider hashicorp/aws: no available releases match the given constraints >= 2.23.0, >= 4.33.0, >= 5.0.0, ~>
│ 5.6.2, >= 5.95.0, < 6.0.0
│ 
│ To see which modules are currently depending on hashicorp/aws and what versions are specified, run the following command:
│     terraform providers.

Resolution : 
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = ">= 4.0.0"
    }
  }

  run terraform init -upgrade
  run terraform plan, apploy

  Error: creating EKS Add-On (iac-terraform-eks-5taOxpiS:aws-ebs-csi-driver): operation error EKS: CreateAddon, https response error StatusCode: 400, RequestID: cfd42327-83e8-4e1a-aa77-5494c3daa861, InvalidParameterException: Addon version specified is not supported
│ 
│   with aws_eks_addon.ebs-csi,
│   on main.tf line 125, in resource "aws_eks_addon" "ebs-csi":
│  125: resource "aws_eks_addon" "ebs-csi" {
│ 
╵
╷
│ Error: creating EKS Node Group (iac-terraform-eks-5taOxpiS:consul-group-20260709083645050800000015): operation error EKS: CreateNodegroup, https response error StatusCode: 400, RequestID: d1a57673-21bb-40fc-abf0-03561fb6f401, InvalidParameterException: AMI Type AL2_x86_64 is only supported for kubernetes versions 1.32 or earlier
│ 
│   with module.eks.module.eks_managed_node_group["consul"].aws_eks_node_group.this[0],
│   on .terraform/modules/eks/modules/eks-managed-node-group/main.tf line 395, in resource "aws_eks_node_group" "this":
│  395: resource "aws_eks_node_group" "this" {
│ 
Error: creating EKS Add-On (iac-terraform-eks-5taOxpiS:aws-ebs-csi-driver): operation error EKS: CreateAddon, https response error StatusCode: 400, RequestID: cfd42327-
83e8-4e1a-aa77-5494c3daa861, InvalidParameterException: Addon version specified is not supported                                                                          
│                                                                                                                                                                         
│   with aws_eks_addon.ebs-csi,                                                                                                                                           
│   on main.tf line 125, in resource "aws_eks_addon" "ebs-csi":                                                                                                           
│  125: resource "aws_eks_addon" "ebs-csi" {                                                                                                                              
│             
│ Error: creating EKS Node Group (iac-terraform-eks-5taOxpiS:consul-group-20260709083645050800000015): operation error EKS: CreateNodegroup, https response error StatusCo
de: 400, RequestID: d1a57673-21bb-40fc-abf0-03561fb6f401, InvalidParameterException: AMI Type AL2_x86_64 is only supported for kubernetes versions 1.32 or earlier        
│                                                                                                                                                                         
│   with module.eks.module.eks_managed_node_group["consul"].aws_eks_node_group.this[0],                                                                                   
│   on .terraform/modules/eks/modules/eks-managed-node-group/main.tf line 395, in resource "aws_eks_node_group" "this":                                                   
│  395: resource "aws_eks_node_group" "this" {                                                                                                                            
│   
Resolution : 
# ❌ REMOVE or COMMENT OUT this line:
  # addon_version = "v1.20.0-eksbuild.1" 

  # AWS will now automatically default to the latest compatible version.                                                     

  AMI Type AL2_x86_64 Not Supported

  Resolution :
  # ⬇️ UPDATE THIS LINE ⬇️
      ami_type = "AL2023_x86_64_STANDARD"

terraform apply --auto-approve
random_string.suffix: Refreshing state... [id=5taOxpiS]
data.aws_iam_policy.ebs_csi_policy: Reading...
module.eks.module.eks_managed_node_group["consul"].data.aws_partition.current: Reading...
module.eks.data.aws_caller_identity.current[0]: Reading...
module.eks.module.kms.data.aws_caller_identity.current[0]: Reading...
module.irsa-ebs-csi.data.aws_partition.current: Reading...
module.irsa-ebs-csi.data.aws_caller_identity.current: Reading...
module.eks.module.eks_managed_node_group["consul"].data.aws_caller_identity.current: Reading...
module.eks.data.aws_iam_policy_document.assume_role_policy[0]: Reading...
module.eks.aws_cloudwatch_log_group.this[0]: Refreshing state... [id=/aws/eks/iac-terraform-eks-5taOxpiS/cluster]
module.vpc.aws_vpc.this[0]: Refreshing state... [id=vpc-072718ec2f901b8a2]
module.eks.module.eks_managed_node_group["consul"].data.aws_partition.current: Read complete after 0s [id=aws]
module.irsa-ebs-csi.data.aws_partition.current: Read complete after 0s [id=aws]
module.eks.data.aws_iam_policy_document.assume_role_policy[0]: Read complete after 0s [id=2830595799]
module.eks.data.aws_partition.current[0]: Reading...
data.aws_availability_zones.available: Reading...
module.eks.module.kms.data.aws_partition.current[0]: Reading...
module.eks.data.aws_partition.current[0]: Read complete after 0s [id=aws]
module.eks.module.kms.data.aws_partition.current[0]: Read complete after 0s [id=aws]
module.eks.module.eks_managed_node_group["consul"].data.aws_iam_policy_document.assume_role_policy[0]: Reading...
module.eks.module.eks_managed_node_group["consul"].data.aws_iam_policy_document.assume_role_policy[0]: Read complete after 0s [id=2560088296]
module.eks.aws_iam_role.this[0]: Refreshing state... [id=iac-terraform-eks-5taOxpiS-cluster-20260709082704104400000002]
module.eks.module.eks_managed_node_group["consul"].aws_iam_role.this[0]: Refreshing state... [id=consul-group-eks-node-group-20260709082704104400000001]
module.irsa-ebs-csi.data.aws_caller_identity.current: Read complete after 0s [id=863852787437]
module.eks.data.aws_iam_policy_document.custom[0]: Reading...
module.eks.data.aws_iam_policy_document.custom[0]: Read complete after 0s [id=513122117]
module.eks.aws_iam_policy.custom[0]: Refreshing state... [id=arn:aws:iam::863852787437:policy/iac-terraform-eks-5taOxpiS-cluster-20260709082704104500000003]
module.eks.data.aws_caller_identity.current[0]: Read complete after 0s [id=863852787437]
module.eks.data.aws_iam_session_context.current[0]: Reading...
module.eks.data.aws_iam_session_context.current[0]: Read complete after 0s [id=arn:aws:iam::863852787437:user/iac-terraform-aws]
module.eks.module.eks_managed_node_group["consul"].data.aws_caller_identity.current: Read complete after 0s [id=863852787437]
module.eks.module.kms.data.aws_caller_identity.current[0]: Read complete after 1s [id=863852787437]
data.aws_availability_zones.available: Read complete after 1s [id=us-east-2]
data.aws_iam_policy.ebs_csi_policy: Read complete after 1s [id=arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy]
module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["AmazonEKSWorkerNodePolicy"]: Refreshing state... [id=consul-group-eks-node-group-20260709082704104400000001-20260709082706289900000004]
module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["AmazonEC2ContainerRegistryReadOnly"]: Refreshing state... [id=consul-group-eks-node-group-20260709082704104400000001-20260709082706302400000005]
module.eks.module.eks_managed_node_group["consul"].aws_iam_role_policy_attachment.this["AmazonEKS_CNI_Policy"]: Refreshing state... [id=consul-group-eks-node-group-20260709082704104400000001-20260709082706367400000006]
module.eks.aws_iam_role_policy_attachment.this["AmazonEKSClusterPolicy"]: Refreshing state... [id=iac-terraform-eks-5taOxpiS-cluster-20260709082704104400000002-20260709082706608300000008]
module.eks.aws_iam_role_policy_attachment.this["AmazonEKSVPCResourceController"]: Refreshing state... [id=iac-terraform-eks-5taOxpiS-cluster-20260709082704104400000002-20260709082706599100000007]
module.eks.aws_iam_role_policy_attachment.custom[0]: Refreshing state... [id=iac-terraform-eks-5taOxpiS-cluster-20260709082704104400000002-20260709082706703800000009]
module.eks.module.kms.data.aws_iam_policy_document.this[0]: Reading...
module.eks.module.kms.data.aws_iam_policy_document.this[0]: Read complete after 0s [id=2017448144]
module.eks.module.kms.aws_kms_key.this[0]: Refreshing state... [id=86c14d60-994d-4dc9-b33c-01ff4a19e4bf]
module.eks.aws_iam_policy.cluster_encryption[0]: Refreshing state... [id=arn:aws:iam::863852787437:policy/iac-terraform-eks-5taOxpiS-cluster-ClusterEncryption2026070908273364220000000f]
module.eks.module.kms.aws_kms_alias.this["cluster"]: Refreshing state... [id=alias/eks/iac-terraform-eks-5taOxpiS]
module.vpc.aws_default_security_group.this[0]: Refreshing state... [id=sg-0820a64384a90635c]
module.eks.aws_security_group.node[0]: Refreshing state... [id=sg-0e1de1a8eae3d0b71]
module.vpc.aws_route_table.public[0]: Refreshing state... [id=rtb-0747e173c9bc23bd0]
module.vpc.aws_route_table.private[0]: Refreshing state... [id=rtb-0cde0961a9421d846]
module.eks.aws_security_group.cluster[0]: Refreshing state... [id=sg-06ed66ca998f5876e]
module.vpc.aws_default_network_acl.this[0]: Refreshing state... [id=acl-0579862dfe490b0ee]
module.vpc.aws_default_route_table.default[0]: Refreshing state... [id=rtb-05c7e388f713e420a]
module.vpc.aws_internet_gateway.this[0]: Refreshing state... [id=igw-06fe6f89c1f708d9e]
module.vpc.aws_subnet.public[2]: Refreshing state... [id=subnet-0c75f28cb52cf8cd1]
module.vpc.aws_subnet.public[0]: Refreshing state... [id=subnet-0dfd1afe1f8a48ee9]
module.vpc.aws_subnet.public[1]: Refreshing state... [id=subnet-0968a68d249d8d581]
module.vpc.aws_subnet.private[0]: Refreshing state... [id=subnet-03c1b9e43d0848af4]
module.vpc.aws_subnet.private[1]: Refreshing state... [id=subnet-0c74bfd8eedb2c9bc]
module.vpc.aws_subnet.private[2]: Refreshing state... [id=subnet-096bd3c76fb9a1f1b]
module.eks.aws_iam_role_policy_attachment.cluster_encryption[0]: Refreshing state... [id=iac-terraform-eks-5taOxpiS-cluster-20260709082704104400000002-20260709082734912400000010]
module.eks.aws_security_group_rule.cluster["ingress_nodes_443"]: Refreshing state... [id=sgrule-3118809019]
module.eks.aws_security_group_rule.node["ingress_self_coredns_udp"]: Refreshing state... [id=sgrule-639658766]
module.eks.aws_security_group_rule.node["ingress_cluster_8443_webhook"]: Refreshing state... [id=sgrule-501143255]
module.eks.aws_security_group_rule.node["ingress_cluster_443"]: Refreshing state... [id=sgrule-1497178920]
module.eks.aws_security_group_rule.node["egress_all"]: Refreshing state... [id=sgrule-3729569434]
module.eks.aws_security_group_rule.node["ingress_cluster_4443_webhook"]: Refreshing state... [id=sgrule-3351285088]
module.eks.aws_security_group_rule.node["ingress_cluster_6443_webhook"]: Refreshing state... [id=sgrule-243460854]
module.eks.aws_security_group_rule.node["ingress_self_all"]: Refreshing state... [id=sgrule-1617812755]
module.eks.aws_security_group_rule.node["ingress_cluster_9443_webhook"]: Refreshing state... [id=sgrule-2038424860]
module.eks.aws_security_group_rule.node["ingress_nodes_ephemeral"]: Refreshing state... [id=sgrule-169284640]
module.eks.aws_security_group_rule.node["ingress_self_coredns_tcp"]: Refreshing state... [id=sgrule-2189412577]
module.eks.aws_security_group_rule.node["ingress_cluster_all"]: Refreshing state... [id=sgrule-281679122]
module.eks.aws_security_group_rule.node["ingress_cluster_kubelet"]: Refreshing state... [id=sgrule-1969786865]
module.vpc.aws_eip.nat[0]: Refreshing state... [id=eipalloc-0948987c08785214f]
module.vpc.aws_route.public_internet_gateway[0]: Refreshing state... [id=r-rtb-0747e173c9bc23bd01080289494]
.
module.vpc.aws_nat_gateway.this[0]: Refreshing state... [id=nat-09d2821f5f2da1292]
module.eks.aws_eks_cluster.this[0]: Refreshing state... [id=iac-terraform-eks-5taOxpiS]
module.vpc.aws_route.private_nat_gateway[0]: Refreshing state... [id=r-rtb-0cde0961a9421d8461080289494]
data.aws_eks_cluster_auth.cluster: Reading...
module.eks.time_sleep.this[0]: Refreshing state... [id=2026-07-09T08:36:36Z]
data.aws_eks_cluster.cluster: Reading...
module.irsa-ebs-csi.data.aws_iam_policy_document.assume_role_with_oidc[0]: Reading...
data.aws_eks_cluster_auth.cluster: Read complete after 0s [id=iac-terraform-eks-5taOxpiS]
module.eks.data.tls_certificate.this[0]: Reading...
module.irsa-ebs-csi.data.aws_iam_policy_document.assume_role_with_oidc[0]: Read complete after 0s [id=3019152076]
module.irsa-ebs-csi.aws_iam_role.this[0]: Refreshing state... [id=AmazonEKSTFEBSCSIRole-iac-terraform-eks-5taOxpiS]
module.eks.module.eks_managed_node_group["consul"].module.user_data.null_resource.validate_cluster_service_cidr: Refreshing state... [id=4882615177983612174]
module.eks.module.eks_managed_node_group["consul"].aws_launch_template.this[0]: Refreshing state... [id=lt-0d9d4dac067b513e7]
data.aws_eks_cluster.cluster: Read complete after 0s [id=iac-terraform-eks-5taOxpiS]
module.eks.data.tls_certificate.this[0]: Read complete after 0s [id=033a163afb2babc26f7883e642621ac361c93d61]
module.eks.aws_iam_openid_connect_provider.oidc_provider[0]: Refreshing state... [id=arn:aws:iam::863852787437:oidc-provider/oidc.eks.us-east-2.amazonaws.com/id/AEB3F6B85CEDD990270FEAABE17ABB75]
module.irsa-ebs-csi.aws_iam_role_policy_attachment.custom[0]: Refreshing state... [id=AmazonEKSTFEBSCSIRole-iac-terraform-eks-5taOxpiS-20260709083609516600000012]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_eks_addon.ebs-csi will be created
  + resource "aws_eks_addon" "ebs-csi" {
      + addon_name               = "aws-ebs-csi-driver"
      + addon_version            = (known after apply)
      + arn                      = (known after apply)
      + cluster_name             = "iac-terraform-eks-5taOxpiS"
      + configuration_values     = (known after apply)
      + created_at               = (known after apply)
      + id                       = (known after apply)
      + modified_at              = (known after apply)
      + service_account_role_arn = "arn:aws:iam::863852787437:role/AmazonEKSTFEBSCSIRole-iac-terraform-eks-5taOxpiS"
      + tags                     = {
          + "eks_addon" = "ebs-csi"
          + "terraform" = "true"
        }
      + tags_all                 = {
          + "eks_addon" = "ebs-csi"
          + "terraform" = "true"
        }
    }

  # module.eks.module.eks_managed_node_group["consul"].aws_eks_node_group.this[0] will be created
  + resource "aws_eks_node_group" "this" {
      + ami_type               = "AL2023_x86_64_STANDARD"
      + arn                    = (known after apply)
      + capacity_type          = (known after apply)
      + cluster_name           = "iac-terraform-eks-5taOxpiS"
      + disk_size              = (known after apply)
      + id                     = (known after apply)
      + instance_types         = [
          + "t3a.medium",
        ]
      + node_group_name        = (known after apply)
      + node_group_name_prefix = "consul-group-"
      + node_role_arn          = "arn:aws:iam::863852787437:role/consul-group-eks-node-group-20260709082704104400000001"
      + release_version        = (known after apply)
      + resources              = (known after apply)
      + status                 = (known after apply)
      + subnet_ids             = [
          + "subnet-03c1b9e43d0848af4",
          + "subnet-096bd3c76fb9a1f1b",
          + "subnet-0c74bfd8eedb2c9bc",
        ]
      + tags                   = {
          + "Name" = "consul-group"
        }
      + tags_all               = {
          + "Name" = "consul-group"
        }
      + version                = "1.34"

      + launch_template {
          + id      = "lt-0d9d4dac067b513e7"
          + name    = (known after apply)
          + version = "1"
        }

      + node_repair_config (known after apply)

      + scaling_config {
          + desired_size = 3
          + max_size     = 3
          + min_size     = 1
        }

      + timeouts {}

      + update_config {
          + max_unavailable_percentage = 33
        }
    }

Plan: 2 to add, 0 to change, 0 to destroy.
aws_eks_addon.ebs-csi: Creating...
module.eks.module.eks_managed_node_group["consul"].aws_eks_node_group.this[0]: Creating...
 .
aws_eks_addon.ebs-csi: Still creating... [00m40s elapsed]
module.eks.module.eks_managed_node_group["consul"].aws_eks_node_group.this[0]: Still creating... [00m40s elapsed]
module.eks.module.eks_managed_node_group["consul"].aws_eks_node_group.this[0]: Still creating... [00m50s elapsed]
 .
 
.
module.eks.module.eks_managed_node_group["consul"].aws_eks_node_group.this[0]: Still creating... [20m00s elapsed]
.
module.eks.module.eks_managed_node_group["consul"].aws_eks_node_group.this[0]: Creation complete after 32m59s [id=iac-terraform-eks-5taOxpiS:consul-group-20260709091034638600000002]
╷
│ Warning: Running terraform apply again will remove the kubernetes add-on and attempt to create it again effectively purging previous add-on configuration
│ 
│   with aws_eks_addon.ebs-csi,
│   on main.tf line 126, in resource "aws_eks_addon" "ebs-csi":
│  126: resource "aws_eks_addon" "ebs-csi" {
│ 
╵
╷
│ Error: waiting for EKS Add-On (iac-terraform-eks-5taOxpiS:aws-ebs-csi-driver) create: timeout while waiting for state to become 'ACTIVE' (last state: 'DEGRADED', timeout: 20m0s)
│ 
│   with aws_eks_addon.ebs-csi,
│   on main.tf line 126, in resource "aws_eks_addon" "ebs-csi":
│  126: resource "aws_eks_addon" "ebs-csi" {
│ 
╵
prashantubale@Sams-Mac eks % terraform apply --auto-approve
random_string.suffix: Refreshing state... [id=5taOxpiS]
.
.
Note: Objects have changed outside of Terraform

Terraform detected the following changes made outside of Terraform since the last "terraform apply" which may have affected this plan:

  # module.eks.module.eks_managed_node_group["consul"].aws_eks_node_group.this[0] has changed
  ~ resource "aws_eks_node_group" "this" {
        id                     = "iac-terraform-eks-5taOxpiS:consul-group-20260709091034638600000002"
      + labels                 = {}
        tags                   = {
            "Name" = "consul-group"
        }
        # (15 unchanged attributes hidden)

        # (4 unchanged blocks hidden)
    }


Unless you have made equivalent changes to your configuration, or ignored the relevant attributes using ignore_changes, the following plan
may include actions to undo or respond to these changes.

────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # aws_eks_addon.ebs-csi is tainted, so must be replaced
-/+ resource "aws_eks_addon" "ebs-csi" {
      ~ addon_version            = "v1.62.0-eksbuild.1" -> (known after apply)
      ~ arn                      = "arn:aws:eks:us-east-2:863852787437:addon/iac-terraform-eks-5taOxpiS/aws-ebs-csi-driver/04cfa312-5440-cfc1-524f-bb43159490a0" -> (known after apply)
      + configuration_values     = (known after apply)
      ~ created_at               = "2026-07-09T09:10:35Z" -> (known after apply)
      ~ id                       = "iac-terraform-eks-5taOxpiS:aws-ebs-csi-driver" -> (known after apply)
      ~ modified_at              = "2026-07-09T09:10:56Z" -> (known after apply)
        tags                     = {
            "eks_addon" = "ebs-csi"
            "terraform" = "true"
        }
        # (4 unchanged attributes hidden)
    }

Plan: 1 to add, 0 to change, 1 to destroy.
aws_eks_addon.ebs-csi: Destroying... [id=iac-terraform-eks-5taOxpiS:aws-ebs-csi-driver]
aws_eks_addon.ebs-csi: Destruction complete after 10s
aws_eks_addon.ebs-csi: Creating...

aws_eks_addon.ebs-csi: Creation complete after 36s [id=iac-terraform-eks-5taOxpiS:aws-ebs-csi-driver]

Apply complete! Resources: 1 added, 0 changed, 1 destroyed.

Outputs:

cluster_name = "iac-terraform-eks-5taOxpiS"
region = "us-east-2"
![alt text](<Screenshot 2026-07-09 at 3.26.00 PM.png>)

# Provision an AKS Cluster
open or add new terminal window and cd aks folder
### log in to Azure using the Azure CLI
az login

After successful login create an Active Directory service principal account.
$ az ad sp create-for-rbac --skip-assignment
{
  "appId": "******",
  "displayName": "azure-cli-2021-04-22-17-52-06",
  "name": "http://azure-cli-2021-04-22-17-52-06",
  "password": "************",
  "tenant": "********"
}
Replace appId and password 
### terraform.tfvars
appId    = "*****"
password = "*****"

### terraform init
Initializing provider plugins found in the configuration...

Initializing the backend...

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

## terraform plan

rror: Error ensuring Resource Providers are registered.
│ 
│ Terraform automatically attempts to register the Resource Providers it supports to
│ ensure it's able to provision resources.
│ 
│ If you don't have permission to register Resource Providers you may wish to use the
│ "skip_provider_registration" flag in the Provider block to disable this functionality.
│ 
│ Please note that if you opt out of Resource Provider Registration and Terraform tries
│ to provision a resource from a Resource Provider which is unregistered, then the errors
│ may appear misleading - for example:
│ 
│ > API version 2019-XX-XX was not found for Microsoft.Foo
│ 
│ Could indicate either that the Resource Provider "Microsoft.Foo" requires registration,
│ but this could also indicate that this Azure Region doesn't support this API version.
│ 
│ More information on the "skip_provider_registration" flag can be found here:
│ https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs#skip_provider_registration
│ 
│ Original Error: determining which Required Resource Providers require registration: the required Resource Provider "Microsoft.MixedReality" wasn't returned from the Azure API
│ 
│   with provider["registry.terraform.io/hashicorp/azurerm"],
│   on main.tf line 15, in provider "azurerm":
│   15: provider "azurerm" {

Resolution :

Bypass Provider Registration
provider "azurerm" {
  features {}

  # ⬇️ ADD THIS LINE ⬇️
  skip_provider_registration = true
}
Fix the Missing Provider Check
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 4.0" # Or the latest 3.x release
    }
  }
}

Then run terraform init -upgrade to apply the update.
terraform init, and plan
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_kubernetes_cluster.default will be created
  + resource "azurerm_kubernetes_cluster" "default" {
      + ai_toolchain_operator_enabled       = false
      + current_kubernetes_version          = (known after apply)
      + dns_prefix                          = (known after apply)
      + fqdn                                = (known after apply)
      + http_application_routing_zone_name  = (known after apply)
      + id                                  = (known after apply)
      + kube_admin_config                   = (sensitive value)
      + kube_admin_config_raw               = (sensitive value)
      + kube_config                         = (sensitive value)
      + kube_config_raw                     = (sensitive value)
      + kubernetes_version                  = "1.26.3"
      + location                            = "westus2"
      + name                                = (known after apply)
      + node_os_upgrade_channel             = "NodeImage"
      + node_resource_group                 = (known after apply)
      + node_resource_group_id              = (known after apply)
      + oidc_issuer_enabled                 = (known after apply)
      + oidc_issuer_url                     = (known after apply)
      + portal_fqdn                         = (known after apply)
      + private_cluster_enabled             = false
      + private_cluster_public_fqdn_enabled = false
      + private_dns_zone_id                 = (known after apply)
      + private_fqdn                        = (known after apply)
      + resource_group_name                 = (known after apply)
      + role_based_access_control_enabled   = true
      + run_command_enabled                 = true
      + sku_tier                            = "Free"
      + support_plan                        = "KubernetesOfficial"
      + tags                                = {
          + "environment" = "Dev"
        }
      + workload_identity_enabled           = false

      + auto_scaler_profile (known after apply)

      + bootstrap_profile (known after apply)

      + default_node_pool {
          + kubelet_disk_type    = (known after apply)
          + max_pods             = (known after apply)
          + name                 = "default"
          + node_count           = 3
          + node_labels          = (known after apply)
          + orchestrator_version = (known after apply)
          + os_disk_size_gb      = 30
          + os_disk_type         = "Managed"
          + os_sku               = (known after apply)
          + scale_down_mode      = "Delete"
          + type                 = "VirtualMachineScaleSets"
          + ultra_ssd_enabled    = false
          + vm_size              = "Standard_D2_v2"
          + workload_runtime     = (known after apply)
        }

      + kubelet_identity (known after apply)

      + network_profile (known after apply)

      + node_provisioning_profile (known after apply)

      + service_principal {
          + client_id     = "a0b385d1-4fbd-45dc-9d3b-fdeb9cfb98d2"
          + client_secret = (sensitive value)
        }

      + windows_profile (known after apply)
    }

  # azurerm_resource_group.default will be created
  + resource "azurerm_resource_group" "default" {
      + id       = (known after apply)
      + location = "westus2"
      + name     = (known after apply)
      + tags     = {
          + "environment" = "Dev"
        }
    }

  # random_pet.prefix will be created
  + resource "random_pet" "prefix" {
      + id        = (known after apply)
      + length    = 2
      + separator = "-"
    }

Plan: 3 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + kubernetes_cluster_name = (known after apply)
  + resource_group_name     = (known after apply)
╷
│ Warning: Argument is deprecated
│ 
│   with provider["registry.terraform.io/hashicorp/azurerm"],
│   on main.tf line 17, in provider "azurerm":
│   17:   skip_provider_registration = true
│ 
│ This property is deprecated and will be removed in v5.0 of the AzureRM provider. Please use the `resource_provider_registrations` property instead.
╵
╷
│ Warning: Attribute Deprecated
│ 
│   with provider["registry.terraform.io/hashicorp/azurerm"],
│   on main.tf line 17, in provider "azurerm":
│   17:   skip_provider_registration = true
│ 
│ This property is deprecated and will be removed in v5.0 of the AzureRM provider. Please use the `resource_provider_registrations` property instead.

Error: creating Kubernetes Cluster (Subscription: "15aab28c-d48a-469e-b70a-853e88871b16"
│ Resource Group Name: "adapting-mongoose-aks"
│ Kubernetes Cluster Name: "adapting-mongoose-aks"): performing CreateOrUpdate: unexpected status 400 (400 Bad Request) with response: {
│   "code": "K8sVersionNotSupported",
│   "details": null,
│   "message": "Managed cluster adapting-mongoose-aks is on version 1.26.3 which is not supported in this region. Please use [az aks get-versions] command to get the supported version list in this region. For more information, please check https://aka.ms/supported-version-list",
│   "subcode": ""
│  }
│ 
│   with azurerm_kubernetes_cluster.default,
│   on main.tf line 29, in resource "azurerm_kubernetes_cluster" "default":
│   29: resource "azurerm_kubernetes_cluster" "default" {

Resolution: az aks get-versions --location "West US 2" --output table
# ⬇️ Update to a supported version ⬇️
  kubernetes_version  = "1.36"

  Error: creating Kubernetes Cluster (Subscription: "15aab28c-d48a-469e-b70a-853e88871b16"
│ Resource Group Name: "adapting-mongoose-aks"
│ Kubernetes Cluster Name: "adapting-mongoose-aks"): performing CreateOrUpdate: unexpected status 400 (400 Bad Request) with response: {
│   "code": "BadRequest",
│   "details": null,
│   "message": "The VM size of Standard_D2_v2 is not allowed in your subscription in location 'westus2'. The available VM sizes are 'standard_b16als_v2,standard_b16as_v2,standard_b16ls_v2,standard_b16pls_v2,standard_b16ps_

Resolution : in location = "East US 2"
 default_node_pool {
    name            = "default"
    node_count      = 2
    vm_size         = "Standard_D4s_v6"
    os_disk_size_gb = 30
  }


Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

kubernetes_cluster_name = "adapting-mongoose-aks"
resource_group_name = "adapting-mongoose-aks"
![alt text](<Screenshot 2026-07-09 at 6.18.32 PM.png>)
