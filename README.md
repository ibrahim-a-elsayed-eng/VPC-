<div align="center">

# Amazon VPC Networking Series (AWS Hands-On Labs)

![AWS](https://img.shields.io/badge/AWS-VPC%20Networking%20Series-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Progress](https://img.shields.io/badge/Progress-2%2F9%20Labs%20Completed-0EA5E9?style=for-the-badge)
![CLI](https://img.shields.io/badge/Tools-Console%20%7C%20CloudShell%20CLI-10B981?style=for-the-badge)
![Cost](https://img.shields.io/badge/Lab%20Cost-%240.00%20Verified-0F172A?style=for-the-badge)

**Hands-on progression through the 9-part Amazon VPC networking series—covering VPC foundations, routing, stateful/stateless security, multi-region visibility, peering, and VPC endpoints.**

</div>

---

## Series Progress (`2 / 9` Completed)

| # | Lab | Key Concepts | Lab Notes | NextWork Proof |
| :---: | :--- | :--- | :--- | :--- |
| 1 | **Build a Virtual Private Cloud** | VPC CIDR, Subnetting, Internet Gateway, CloudShell CLI | [01-build-a-vpc.md](./labs/01-build-a-vpc.md) | [NextWork Doc](https://nextwork.ai/hemaa/docs/7f907ac7-2473-5c15-a8be-edb36581cdba) |
| 2 | **VPC Traffic Flow and Security** | Route Tables, Security Groups (Stateful), NACLs (Stateless), EC2 Global View | [02-vpc-traffic-flow-and-security.md](./labs/02-vpc-traffic-flow-and-security.md) | [NextWork Doc](https://nextwork.ai/hemaa/docs/fe5ed473-5874-57e1-a58f-d9b3d652330c) |
| 3 | Creating a Private Subnet | Private Subnets, Route Table Isolation | *Pending* | — |
| 4 | Launching VPC Resources | EC2 in Public & Private Subnets | *Pending* | — |
| 5 | Testing VPC Connectivity | SSH, Bastion/Jump Host, ICMP/HTTP Testing | *Pending* | — |
| 6 | VPC Peering | Cross-VPC Private Routing | *Pending* | — |
| 7 | VPC Monitoring with Flow Logs | VPC Flow Logs, CloudWatch Logs | *Pending* | — |
| 8 | Access S3 from a VPC | Gateway VPC Endpoints, Private S3 Access | *Pending* | — |
| 9 | Build a VPC with CloudFormation / IaC | Infrastructure as Code VPC Provisioning | *Pending* | — |

---

## Repository Structure

```text
VPC-/
├── README.md                                  # Series overview & progress tracker (2/9)
├── images/
│   └── aws_vpc_part1_architecture.jpg         # Series architecture diagram
└── labs/
    ├── 01-build-a-vpc.md                      # Lab 01: VPC, Subnet, IGW (Console + CLI)
    └── 02-vpc-traffic-flow-and-security.md    # Lab 02: Route Tables, SG, NACL & EC2 Global View
```

---

## Engineering & Cost Guardrails
- **Zero-Spend Teardown:** Every lab is torn down immediately after verification (`$0.00` AWS spend confirmed; no idle NAT Gateways, Elastic IPs, or EC2 instances left running).
- **Secret Hygiene:** Zero AWS Account IDs, real public IPs, or credentials committed.
- **Next Flagship Consolidation:** Upon completing all 9 labs, the full production architecture will be codified in Terraform inside [terraform-aws-vpc](https://github.com/ibrahim-a-elsayed-eng/terraform-aws-vpc).
