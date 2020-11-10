# Cloudendure migration

# 접근 도메인 
 > 1. URL HomePage : https://www.cloudendure.com
 > 2. Login URL : https://console.cloudendure.com

# Cloudendure Policy
~~~
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": "ec2:CreateTags",
      "Resource": "arn:aws:ec2:*:*:*/*",
      "Condition": {
        "StringEquals": {
          "ec2:CreateAction": "RunInstances"
        }
      }
    },
    {
      "Sid": "VisualEditor1",
      "Effect": "Allow",
      "Action": "ec2:CreateTags",
      "Resource": "arn:aws:ec2:*:*:*/*",
      "Condition": {
        "StringEquals": {
          "ec2:CreateAction": "CreateVolume"
        }
      }
    },
    {
      "Sid": "VisualEditor2",
      "Effect": "Allow",
      "Action": [
        "ec2:RevokeSecurityGroupIngress",
        "ec2:DetachVolume",
        "ec2:AttachVolume",
        "ec2:DeleteVolume",
        "ec2:TerminateInstances",
        "ec2:StartInstances",
        "ec2:RevokeSecurityGroupEgress",
        "ec2:StopInstances"
      ],
      "Resource": [
        "arn:aws:ec2:*:*:dhcp-options/*",
        "arn:aws:ec2:*:*:instance/*",
        "arn:aws:ec2:*:*:volume/*",
        "arn:aws:ec2:*:*:security-group/*"
      ],
      "Condition": {
        "StringLike": {
          "ec2:ResourceTag/Name": "CloudEndure*"
        }
      }
    },
    {
      "Sid": "VisualEditor3",
      "Effect": "Allow",
      "Action": [
        "ec2:RevokeSecurityGroupIngress",
        "ec2:DetachVolume",
        "ec2:AttachVolume",
        "ec2:DeleteVolume",
        "ec2:TerminateInstances",
        "ec2:StartInstances",
        "ec2:RevokeSecurityGroupEgress",
        "ec2:StopInstances"
      ],
      "Resource": [
        "arn:aws:ec2:*:*:dhcp-options/*",
        "arn:aws:ec2:*:*:instance/*",
        "arn:aws:ec2:*:*:volume/*",
        "arn:aws:ec2:*:*:security-group/*"
      ],
      "Condition": {
        "StringLike": {
          "ec2:ResourceTag/CloudEndure creation time": "*"
        }
      }
    },
    {
      "Sid": "VisualEditor4",
      "Effect": "Allow",
      "Action": [
        "ec2:DisassociateAddress",
        "ec2:CreateDhcpOptions",
        "ec2:AuthorizeSecurityGroupIngress",
        "ec2:DeregisterImage",
        "ec2:DeleteSubnet",
        "ec2:DeleteSnapshot",
        "ec2:ModifySnapshotAttribute",
        "ec2:ModifyVolumeAttribute",
        "ec2:CreateVpc",
        "ec2:AttachInternetGateway",
        "ec2:GetConsoleScreenshot",
        "ec2:GetConsoleOutput",
        "elasticloadbalancing:DescribeLoadBalancer*",
        "ec2:CreateRoute",
        "ec2:CreateInternetGateway",
        "ec2:CreateSecurityGroup",
        "ec2:CreateSnapshot",
        "ec2:ModifyVpcAttribute",
        "ec2:ModifyInstanceAttribute",
        "ec2:ReleaseAddress",
        "ec2:AuthorizeSecurityGroupEgress",
        "ec2:AssociateDhcpOptions",
        "ec2:ImportKeyPair",
        "ec2:CreateTags",
        "ec2:RegisterImage",
        "ec2:ModifyNetworkInterfaceAttribute",
        "ec2:AssociateRouteTable",
        "ec2:CreateRouteTable",
        "ec2:DetachInternetGateway",
        "iam:ListInstanceProfiles",
        "ec2:AllocateAddress",
        "ec2:ReplaceNetworkAclAssociation",
        "ec2:CreateVolume",
        "kms:ListKeys",
        "ec2:Describe*",
        "ec2:DeleteVpc",
        "iam:GetUser",
        "ec2:CreateSubnet",
        "ec2:AssociateAddress",
        "ec2:DeleteKeyPair",
        "ec2:CreateNetworkAclEntry"
      ],
      "Resource": "*"
    },
    {
      "Sid": "MigrationHubConfig",
      "Effect": "Allow",
        "Action": [
        "mgh:GetHomeRegion"
      ],
      "Resource": "*"
    },
    {
      "Sid": "VisualEditor5",
      "Effect": "Allow",
        "Action": [
        "ec2:RevokeSecurityGroupIngress",
        "mgh:CreateProgressUpdateStream",
        "kms:Decrypt",
        "kms:Encrypt",
        "ec2:RevokeSecurityGroupEgress",
        "ec2:DeleteDhcpOptions",
        "ec2:RunInstances",
        "kms:DescribeKey",
        "kms:CreateGrant",
        "ec2:DeleteNetworkAclEntry",
        "kms:ReEncrypt*",
        "kms:GenerateDataKey*"
      ],
      "Resource": [
        "arn:aws:mgh:*:*:progressUpdateStream/*",
        "arn:aws:ec2:*:*:subnet/*",
        "arn:aws:ec2:*:*:key-pair/*",
        "arn:aws:ec2:*:*:dhcp-options/*",
        "arn:aws:ec2:*:*:instance/*",
        "arn:aws:ec2:*:*:volume/*",
        "arn:aws:ec2:*:*:security-group/*",
        "arn:aws:ec2:*:*:network-acl/*",
        "arn:aws:ec2:*:*:placement-group/*",
        "arn:aws:ec2:*:*:vpc/*",
        "arn:aws:ec2:*:*:network-interface/*",
        "arn:aws:ec2:*::image/*",
        "arn:aws:ec2:*:*:snapshot/*",
        "arn:aws:kms:*:*:key/*"
      ]
    },
    {
      "Sid": "VisualEditor6",
      "Effect": "Allow",
      "Action": [
        "ec2:CreateTags",
        "mgh:ImportMigrationTask",
        "mgh:AssociateCreatedArtifact",
        "mgh:NotifyMigrationTaskState",
        "mgh:DisassociateCreatedArtifact",
        "mgh:PutResourceAttributes"
      ],
      "Resource": [
        "arn:aws:mgh:*:*:progressUpdateStream/*/migrationTask/*",
        "arn:aws:ec2:*:*:subnet/*",
        "arn:aws:ec2:*::network-interface/*",
        "arn:aws:ec2:*:*:dhcp-options/*",
        "arn:aws:ec2:*::snapshot/*",
        "arn:aws:ec2:*:*:security-group/*",
        "arn:aws:ec2:*::image/*"
      ]
    },
    {
      "Sid": "VisualEditor7",
      "Effect": "Allow",
      "Action": "ec2:Delete*",
      "Resource": [
        "arn:aws:ec2:*:*:route-table/*",
        "arn:aws:ec2:*:*:dhcp-options/*",
        "arn:aws:ec2:*:*:instance/*",
        "arn:aws:ec2:*:*:volume/*",
        "arn:aws:ec2:*:*:security-group/*",
        "arn:aws:ec2:*:*:internet-gateway/*"
      ],
      "Condition": {
        "StringLike": {
          "ec2:ResourceTag/Name": "CloudEndure*"
        }
      }
    },
    {
      "Sid": "VisualEditor8",
      "Effect": "Allow",
      "Action": "ec2:Delete*",
      "Resource": [
        "arn:aws:ec2:*:*:route-table/*",
        "arn:aws:ec2:*:*:dhcp-options/*",
        "arn:aws:ec2:*:*:instance/*",
        "arn:aws:ec2:*:*:volume/*",
        "arn:aws:ec2:*:*:security-group/*",
        "arn:aws:ec2:*:*:internet-gateway/*"
      ],
      "Condition": {
        "StringLike": {
          "ec2:ResourceTag/CloudEndure creation time": "*"
        }
      }
    }
  ]
}

~~~

