
[![Linux](https://img.shields.io/badge/OS-Ubuntu_WSL2-orange?logo=ubuntu&logoColor=white)](https://ubuntu.com)
[![Cloud](https://img.shields.io/badge/Cloud-AWS-232F3E?logo=amazonaws&logoColor=white)](https://aws.amazon.com)
[![Shell](https://img.shields.io/badge/Shell-Bash-green?logo=gnubash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Git](https://img.shields.io/badge/Tool-Git-red?logo=git&logoColor=white)](https://git-scm.com)
# 🌐 Custom AWS VPC Architecture & CLI Automation


## 📝 Project Overview / نبذة عن المشروع
This project showcases the creation of a secure, custom Virtual Private Cloud (VPC) on AWS using both the AWS Management Console and CLI automation. The goal was to understand foundational cloud networking, subnets, route tables, and internet connectivity.
في هذا المشروع، قمت ببناء شبكة افتراضية خاصة ومخصصة (VPC) على منصة AWS باستخدام لوحة التحكم والـ CLI. الهدف الأساسي كان فهم وتطبيق أساسيات شبكات السحابية، الشبكات الفرعية، جداول التوجيه، وتوصيل الشبكة بالإنترنت.

---

## 🛠️ Tech Stack / التقنيات المستخدمة
- **Cloud Provider:** AWS (VPC, Subnets, Internet Gateway, Route Tables)
- **Local Environment:** Windows Subsystem for Linux (WSL - Ubuntu)
- **Tooling:** AWS CLI & AWS Management Console

---

## 🗺️ Architecture & IP Schema / هيكلية الشبكة
- **VPC CIDR:** `10.0.0.0/16`
- **Public Subnet:** `10.0.1.0/24` (Configured for public web resources)
- **Internet Gateway (IGW):** Attached to route outbound traffic directly to the internet.

---

## 💻 Step-by-Step Execution / خطوات التنفيذ بالتفصيل

### 1. Building via AWS Console (طريقة لوحة التحكم)
- Created the VPC with the CIDR block `10.0.0.0/16`.
- Provisioned the subnets and configured routing.

### 2. Secret Mission: CLI & WSL Integration (المهمة السرية: تطبيق الأوامر)
To simulate real-world DevOps environments, I successfully used AWS CLI on WSL to configure network resources:
لمحاكاة بيئات العمل الحقيقية، قمت بتنفيذ الأوامر التالية برمجياً عبر سطر الأوامر:
- **Create VPC:**
  ```bash
  aws ec2 create-vpc --cidr-block 10.0.0.0/16
  ```
- **Attach Internet Gateway:**
  ```bash
  aws ec2 attach-internet-gateway --vpc-id <vpc-id> --internet-gateway-id <igw-id>
  ```

---

## 🧠 Lessons Learned & Troubleshooting / التحديات وحلول المشكلات
One of the most valuable parts of this project was debugging real-world CLI configuration hurdles:

1. **The `vpc-` Prefix Omission (خطأ بادئة المعرّف):**
   - *Challenge:* Faced `InvalidVpcID.NotFound` error when executing CLI commands.
   - *Solution:* Realized AWS expects the unique identifier to explicitly include the `vpc-` prefix. Paying close attention to syntax is critical for automation.

2. **Default vs. Custom VPCs (الشبكات الافتراضية والمخصصة):**
   - Learned the core difference between AWS Default VPCs (pre-configured for quick deployment) and Custom VPCs (configured from scratch for production-level security).

---

## 🧹 Cost Optimization & Cleanup / تدمير الموارد وتوفير التكاليف
Following best cloud practices, all created resources were completely torn down after validation to ensure no orphaned resources or public IP charges accrued:
اتباعاً لأفضل ممارسات السحابة، تم حذف وتدمير كافة الموارد بنجاح لتجنب أي تكاليف:
- Detached and deleted the Internet Gateway.
- Deleted all associated custom Subnets.
- Deleted the Custom VPC
- 
