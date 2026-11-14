<img width="2814" height="1536" alt="Gemini_Generated_Image_xwa2mmxwa2mmxwa2" src="https://github.com/user-attachments/assets/ed3eccd3-0d98-4b33-a95a-3ce8147baa9c" />

[![Cloud](https://img.shields.io/badge/Cloud-AWS-232F3E?logo=amazonaws&logoColor=white)](https://aws.amazon.com)
[![Shell](https://img.shields.io/badge/Shell-AWS_CloudShell-orange)](https://aws.amazon.com/cloudshell/)
[![Tool](https://img.shields.io/badge/Tool-AWS_CLI-green)](https://aws.amazon.com/cli/)
[![Tool](https://img.shields.io/badge/Tool-Git-red?logo=git&logoColor=white)](https://git-scm.com)

# 🌐 My First AWS VPC: Console & CLI

## 📝 Project Overview / نبذة عن المشروع
In this NextWork project I took my first steps in AWS networking. I created a Virtual Private Cloud (VPC), a subnet and an internet gateway (IGW) in the AWS Management Console. Then I repeated the same setup with the AWS CLI in CloudShell (Secret Mission).

في هذا المشروع أنشأت أول شبكة افتراضية خاصة (VPC) على AWS مع شبكة فرعية (Subnet) وبوابة إنترنت (IGW) من لوحة التحكم. ثم كررت نفس الإعداد بالأوامر في CloudShell.

## 🛠️ Tech Stack / التقنيات المستخدمة
- **Cloud:** AWS (VPC, Subnet, Internet Gateway)
- **Tools:** AWS Management Console, AWS CloudShell, AWS CLI
- **Documentation:** Git & GitHub

## 🗺️ What I Built / ما قمت ببنائه

| Method | VPC | Subnet | Internet Gateway |
|--------|-----|--------|------------------|
| Console | `NextWork VPC` (`10.0.0.0/16`) | `Public 1` (`10.0.0.0/24`) | `NextWork IG` (attached) |
| CLI | `NextWork VPC 2` (`10.0.0.0/24`) | `10.0.0.0/25` | attached |

> [!NOTE]
> The subnet is named "Public 1", but it only becomes truly public after a route to the internet gateway is added. I will do that in the next project of the series.

## 💻 Steps / الخطوات

### 1. AWS Console
1. Created the VPC `NextWork VPC` with CIDR `10.0.0.0/16`.
2. Created the subnet `Public 1` with CIDR `10.0.0.0/24` and enabled auto-assign public IPv4.
3. Created the internet gateway `NextWork IG` and attached it to the VPC.

### 2. Secret Mission: AWS CLI in CloudShell
```
aws ec2 create-vpc --cidr-block 10.0.0.0/24 --query Vpc.VpcId --output text
aws ec2 create-tags --resources <vpc-id> --tags Key=Name,Value="NextWork VPC 2"
aws ec2 create-subnet --vpc-id <vpc-id> --cidr-block 10.0.0.0/25
aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text
aws ec2 attach-internet-gateway --vpc-id <vpc-id> --internet-gateway-id <igw-id>
```

## 📸 Screenshots / لقطات الشاشة
![VPC settings](vpc%20set.PNG)
![Subnet created](creating%20puplic%20subnet.PNG)
![Internet gateway attached](attached%20IGW%20with%20subnet.PNG)

## 🐞 Challenges & Troubleshooting / التحديات وحلول المشكلات

| Problem | Diagnosis | Solution |
|---------|-----------|----------|
| `InvalidVpcId.Malformed` and `InvalidInternetGatewayId.Malformed` | I copied the IDs without their prefix (`vpc-`, `igw-`) | Used the full IDs, for example `vpc-0d0cc075...` |
| `create-tags` failed | I left the placeholder `VPC-ID` in the command | Replaced it with my real VPC ID |
| `create-subnet` failed | I forgot `--cidr-block` and misspelled some options (`--cidr-bloc`) | Added the option and fixed the spelling |

**Lesson / الدرس:** Read the command slowly, replace every placeholder, and use `--help` to check option names.

## 🧹 Cost & Cleanup / التكلفة والتنظيف
- A VPC, subnets and an internet gateway are free. I did not create any NAT gateway, EC2 instance or public IP.
- The resources are still in my account. I will delete them after I finish the VPC series: detach and delete the internet gateway, then the subnet, then the VPC.
- I also set up a budget alert on my AWS account.

## 🎓 NextWork Project
[View my project page](https://nextwork.ai/hemaa/docs/7f907ac7-2473-5c15-a8be-edb36581cdba)
