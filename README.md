<div align="center">

<img alt="AWS VPC Part 1 Architecture Diagram" src="./images/aws_vpc_part1_architecture.jpg" />

# My First AWS VPC: Console & CLI

![AWS](https://img.shields.io/badge/AWS-VPC%20%7C%20Subnet%20%7C%20IGW-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![CLI](https://img.shields.io/badge/CLI-AWS%20CloudShell-0EA5E9?style=for-the-badge&logo=amazonaws&logoColor=white)
![Networking](https://img.shields.io/badge/Networking-CIDR%2010.0.0.0%2F16-10B981?style=for-the-badge)
![Cost](https://img.shields.io/badge/Lab%20Cost-%240%20Free%20Tier-0F172A?style=for-the-badge)

**Built an AWS Virtual Private Cloud, Subnet, and Internet Gateway using both the AWS Management Console and AWS CloudShell CLI.**

</div>

---

## 1. Architecture Overview

```mermaid
flowchart LR
    IGW["Internet Gateway\nNextWork IG (Attached)"] <--> VPC["VPC: NextWork VPC\n10.0.0.0/16 (Console)"]
    VPC --> Subnet["Subnet: Public 1\n10.0.0.0/24\nAuto-assign Public IPv4: On"]
```

> [!IMPORTANT]
> **Key Design Decision:** Building the same VPC topology twice—first in the AWS Console (`NextWork VPC`) and then via AWS CLI in CloudShell (`NextWork VPC 2`)—validates both visual networking concepts and repeatable CLI provisioning. Note that `Public 1` only becomes truly public after adding a route to the Internet Gateway in the next project of the VPC series.

---

## 2. Problem & Solution

| Aspect | Detail |
| :--- | :--- |
| **Problem** | Default VPCs abstract away how IP ranges (`CIDR`), subnets, and internet gateways actually connect together. |
| **Solution** | Provisioned a custom VPC, subnet, and attached Internet Gateway manually in the AWS Console, then replicated the setup via AWS CloudShell CLI. |
| **Networking Scope** | Console: `NextWork VPC` (`10.0.0.0/16`) + `Public 1` (`10.0.0.0/24`) + `NextWork IG`; CLI: `NextWork VPC 2` (`10.0.0.0/24`) + `10.0.0.0/25` + attached IGW. |

---

## 3. Tech Stack
- **Cloud:** Amazon Web Services (VPC, Subnets, Internet Gateway)
- **Tools:** AWS Management Console, AWS CloudShell, AWS CLI
- **Documentation:** Git & GitHub

---

## 4. Implementation Steps (Summary)
1. **AWS Console Setup:** Created `NextWork VPC` (`10.0.0.0/16`), created subnet `Public 1` (`10.0.0.0/24`) with auto-assign public IPv4 enabled, and created & attached `NextWork IG`.
2. **Secret Mission (AWS CloudShell CLI):** Repeated the build using `aws ec2` commands to create `NextWork VPC 2` (`10.0.0.0/24`), a `10.0.0.0/25` subnet, and an attached Internet Gateway.
3. **Troubleshooting & Cost Guardrails:** Resolved CLI resource ID prefix and option spelling issues, and verified `$0` cost (no NAT Gateway, EC2, or standalone public IP created; budget alert active).

<details>
<summary><b>Click to expand AWS CLI commands & troubleshooting log</b></summary>

```bash
aws ec2 create-vpc --cidr-block 10.0.0.0/24 --query Vpc.VpcId --output text
aws ec2 create-tags --resources <vpc-id> --tags Key=Name,Value="NextWork VPC 2"
aws ec2 create-subnet --vpc-id <vpc-id> --cidr-block 10.0.0.0/25
aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text
aws ec2 attach-internet-gateway --vpc-id <vpc-id> --internet-gateway-id <igw-id>
```

| Problem | Diagnosis | Solution |
| :--- | :--- | :--- |
| `InvalidVpcId.Malformed` and `InvalidInternetGatewayId.Malformed` | Copied IDs without their resource prefix (`vpc-`, `igw-`) | Used full IDs (e.g., `vpc-0d0cc075...`) |
| `create-tags` failed | Left placeholder `VPC-ID` in the command | Replaced placeholder with the actual VPC ID |
| `create-subnet` failed | Missing `--cidr-block` / typo `--cidr-bloc` | Fixed option name using `--help` |

</details>

---

## 5. Verification & Results
- **VPC Settings:** ![VPC settings](vpc%20set.PNG)
- **Subnet Created:** ![Subnet created](creating%20puplic%20subnet.PNG)
- **Internet Gateway Attached:** ![Internet gateway attached](attached%20IGW%20with%20subnet.PNG)
- **NextWork Project Page:** [View NextWork Project](https://nextwork.ai/hemaa/docs/7f907ac7-2473-5c15-a8be-edb36581cdba)

---

## 6. Key Engineering Takeaways
- **Subnet Naming vs. Routing:** Naming a subnet `Public 1` does not make it public on its own—an Internet Gateway attachment plus a route table entry (`0.0.0.0/0 -> igw`) is required.
- **CLI Precision:** Always pass full AWS resource prefixes (`vpc-`, `igw-`), replace placeholders, and verify flags with `--help`.
