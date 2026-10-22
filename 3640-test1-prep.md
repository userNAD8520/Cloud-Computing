# 3640 Fall 2026 — Test 1 Prep Guide (Weeks 1–5)

> **Exam snapshot:** 15% of final grade · reported difficulty **Hard** · in-class · heavier weighting on **Weeks 3–5**, questions may come from **labs**.
> **Format:** 20 "select all that apply" (A–F) · 10 short-answer · several written-response (heavy on **VPC** + **bash**) · **2 written on stateless** (one *network*, one *VPC*).

---

## Color / priority legend

| Marker | Meaning |
|---|---|
| 🔴 **W4 / VPC** | Highest priority + explicit exam emphasis |
| 🟠 **W3 / W5 / Labs** | High priority (heavier weighting) |
| 🟡 **W1 / W2** | Foundational, lighter weighting |
| 🚩 | Matches reported exam emphasis (**VPC, stateless, bash**) |
| ⚠️ | Common mistake / exam trap / quirk |
| 🔧 | **Reconstructed** (source chapter not uploaded — verify against your O'Reilly copy) |

---

# Part 0 — Source errors, quirks & inconsistencies (explicitly flagged)

1. **README:** Week 2 (Ch 5) and Week 3 (Ch 7) readings are external O'Reilly links, **not uploaded** → reconstructed below (🔧).
2. **`aws-vpc.md` typo:** "public **inernet**" → "public internet."
3. **`aws-vpc.md` route-table naming inconsistency:** the lab creates a table **`bcit-demo-rt`** and associates it with the **private** subnet, but then says *"Edit **main route table**, the one auto created → add 0.0.0.0/0 → IGW."* The IGW route actually goes on the **default/main** route table (which the **public** subnet uses because it was never re-associated). Net result is correct (public → IGW; private → no IGW route), but the wording is easy to misread. **No NAT gateway is created**, so the private instance has no outbound internet — fine for the lab, but know what a NAT *would* do.
4. **`vpc.pdf` misleading phrase:** "The *smaller* the CIDR size, the *greater* the number of IP addresses." ⚠️ Correct reading: a **smaller prefix number** (`/16`) = **more** addresses; a larger prefix (`/28`) = fewer. `/28` is the *minimum VPC CIDR* = only 16 addresses.
5. **`aws-cli.md` wording:** prose says `describe-key-pairs` "returns a YAML mapping," but the **default output is JSON** — YAML appears only because that example used `--output yaml`.
6. **`aws-cli.md`:** `aws login` / `aws login --remote` are **new AWS CLI v2** browser-flow commands (IAM Identity Center style). Older docs/VMs won't have them. Never `aws login` as **root**.
7. **`aws-cli.md` import script:** output is redirected to a file literally named `key_data` (no filename variable); the duplicate check relies on `--key-names` **failing** when the key is absent (handled by `&>/dev/null` + `if`).
8. **`aws-ec2.md`:** `ssh-keygen -f .ssh/aws` requires the `.ssh` directory to **already exist** — `ssh-keygen` does not create it.
9. **`aws-ec2.md` cloud-init starter:** `write_files:` is left **empty** (the task); `permissions "0644"` must **stay quoted** (unquoted `0644` is parsed as octal integer 420 by YAML 1.1 and can break cloud-init).
10. **`CIDR.pdf`:** text is truncated mid-example (shows only `192.168.1.0`; the second class-C network, e.g. `192.168.2.0`, is missing) — likely an OCR/extraction gap, not course error.
11. **`vms.pdf`:** containers vs VMs is listed under "Additional Resources (not required)." Containers are **Term 4** per README — treat as skim only.

---

# Part 1 — Complete topic list

## 🟡 Week 1 — Cloud fundamentals (lighter weighting)
- [ ] NIST definition of cloud computing; consumption-based pricing
- [ ] Why organizations use cloud: flexibility, security, efficiency, cost
- [ ] Cloud components: servers/VPS, networking, storage
- [ ] Deployment models: **public / community / private / hybrid** (+ on-premises ≠ private cloud)
- [ ] Service models: **IaaS / PaaS / SaaS** (+ examples: EC2, Vercel, Google Docs)
- [ ] **Regions vs Availability Zones** (`us-west-2`, `ca-central-1`, ≥3 AZs per region)
- [ ] Multitenancy
- [ ] **IaC** (Infrastructure as Code; Terraform/OpenTofu)
- [ ] AWS is a public cloud; AWS + on-prem = hybrid

## 🔧🟡 Week 2 — Security & IAM *(source missing, reconstructed)*
- [ ] IAM: **users, groups, roles, policies**
- [ ] **Root user vs IAM user**; never use root
- [ ] Authentication vs authorization; **MFA**; **least privilege**
- [ ] IAM policy structure (JSON), managed vs inline
- [ ] IAM roles → temporary credentials
- [ ] **AWS Budgeting** (mentioned in `wk01.md`)
- [ ] **Shared Responsibility Model** (AWS vs customer)
- [ ] Security groups (stateful) & NACLs (stateless) — first look

## 🔧🟠 Week 3 — Compute / EC2 *(Ch 7 missing; lab provided)*
- [ ] EC2 concepts: **AMI, instance types, key pairs, security groups**
- [ ] **EBS (persistent) vs instance store (ephemeral)**
- [ ] **Elastic IP vs auto-assigned public IP**
- [ ] Pricing models: on-demand / reserved / spot 🔧
- [ ] 🚩 **SSH**: `ssh-keygen`, `ssh -i`, `known_hosts`, `ssh-keygen -R`
- [ ] 🚩 **cloud-init**: `#cloud-config`, `users`, `packages`, `write_files`, `runcmd`
- [ ] nginx + `curl` test, `cloud-init status --long`

## 🔴 Week 4 — VPC & Networking (highest priority)
- [ ] 🚩 VPC concept; **region-level**; **default vs non-default VPC** (172.31.0.0/16)
- [ ] 🚩 **CIDR**: notation, `/16`–`/28` VPC limit, **RFC 1918** private ranges, **blocked ranges**, classful vs classless, VLSM, **subnetting math**, supernets, usable hosts
- [ ] 🚩 **Subnets**: AZ-level, CIDR subset of VPC, **public vs private subnet**
- [ ] 🚩 **Route tables**: default route `0.0.0.0/0`, main vs custom, subnet associations
- [ ] 🚩 **Internet gateway** (attach to VPC) → makes a subnet *public*
- [ ] 🚩 **NAT** (what it does — not in lab, but exam-relevant)
- [ ] 🚩 **Security groups** (stateful, instance-level) vs **NACLs** (stateless, subnet-level)
- [ ] DNS hostnames setting; auto-assign public IPv4
- [ ] **VPC peering**, **VPN (virtual private gateway + customer gateway, AES 128/256)**, **Direct Connect**
- [ ] *(skim — in uploaded PDF but README says out of scope):* Route 53, CloudFront

## 🟠 Week 5 — AWS CLI + Bash (high priority)
- [ ] AWS CLI **v1 vs v2**; install; `$HOME/.local/bin` on PATH; `aws --version`; tab completion
- [ ] `aws login` / `--remote`; **~/.aws config & credentials**; **profiles**; region `us-west-2`
- [ ] 🚩 Command structure: `aws <service> <subcommand> [options]`
- [ ] 🚩 `--output text|yaml|json`; `--query` **JMESPath** (projection `[*]`, `[-1]`, `sort_by`, pipes `|`)
- [ ] `describe/create/import/delete-key-pair`; `describe-images` + `--filters`
- [ ] 🚩 `file://` vs `fileb://`
- [ ] 🚩 **Bash**: shebang, `set -euo pipefail`, variables, `$# $1 $*`, **command substitution `$( )`**, **heredoc `<<EOF`**, `if [[ ]]` tests (`-f`, `-ne`), functions + `local`, stderr `>&2`, `&>/dev/null`, `exit`, ANSI color
- [ ] Full script walkthroughs: import-key script, get-latest-AMI script

## 🟠 Labs (all higher priority)
- [ ] 🟠 W1 lab: **Linux env** (WSL vs VM vs distrobox; WSL `/mnt/c` filesystem gotcha)
- [ ] 🟠 W3 lab: **EC2** (SSH key import, cloud-init nginx server, curl test)
- [ ] 🔴 W4 lab: **VPC build** (VPC + 2 subnets + RT + IGW + public/private EC2)
- [ ] 🟠 W5 lab: **CLI** (get Debian AMI, import SSH key)

## 🚩 Cross-cutting
- [ ] 🚩 **Stateless vs stateful** — network (HTTP) **and** VPC (NACL vs SG)

---

# Part 2 — Comprehensive study guide

## 🟡 Week 1 — Cloud computing fundamentals

**NIST definition (memorize the shape of it):** cloud is a model for **on-demand**, **ubiquitous**, **convenient** network access to a **shared pool of configurable computing resources** that can be **rapidly provisioned and released** with minimal management effort or provider interaction.

**Pricing:** most cloud services use **consumption-based pricing** — you pay for what you use. ⚠️ Pricing models *vary between services* (don't assume one model fits all).

**Why organizations adopt cloud:** Flexibility (access anywhere, integrated service suites) · Security (dedicated provider security teams) · Efficiency (provision quickly, experiment fast) · Cost (often cheaper than owning hardware).

**Cloud components:**
- **Servers** — powerful machines in data centers; often run multiple VMs, each giving a **VPS**.
- **Networking** — load balancers, switches, connectivity between workloads/data centers.
- **Storage** — persistent, scalable, internet-accessible data.

### Deployment models

| Model | Operator | Tenancy | Example |
|---|---|---|---|
| **Public** | 3rd-party CSP | shared on-demand | AWS, GCP, Azure |
| **Community** | one/more orgs or 3rd party | shared among similar-need orgs | consortium of govt agencies |
| **Private** | single org | dedicated/isolated | corporate cloud (on-prem *or* hosted) |
| **Hybrid** | combined public + private | mixed | on-prem data center + AWS |

⚠️ **Traps:** "On-premises" only means the org manages its own local hardware — it does **not** automatically mean "private cloud" (private cloud implies on-demand self-service). A private cloud also does **not** have to be on-premises. **AWS is a public cloud**; AWS + your on-prem = **hybrid**.

### Service models

| Model | You manage | Provider manages | Example |
|---|---|---|---|
| **IaaS** | OS and up (full control) | hardware/hypervisor | **EC2**, VPS |
| **PaaS** | app + data only | runtime/platform | **Vercel**, Elastic Beanstalk |
| **SaaS** | (end user) | everything | **Google Docs**, Gmail |

⚠️ **Trap:** most AWS services are **IaaS** (highest control, closest to on-prem). The exam loves "which model is EC2?" → **IaaS**.

### Regions vs Availability Zones

| Concept | What it is | Example |
|---|---|---|
| **Region** | geographic area of cloud infrastructure | `us-west-2` (Oregon), `ca-central-1` (Canada) |
| **Availability Zone (AZ)** | isolated location *within* a region, ≥1 data centers | `us-west-2a`, `us-west-2b` |

⚠️ Each AWS Region has **at least three AZs**. Multiple AZs → high availability & fault tolerance. ⚠️ A **VPC is region-level**; a **subnet is AZ-level** (Week 4).

### Multitenancy & IaC

- **Multitenancy** — many customers (tenants) share physical infra while being **logically isolated** (via access controls, virtualization, network isolation, encryption).
- **IaC** — provision/support infra **using code** instead of manual steps; you declare the **desired state** (not the steps). Example: **Terraform** (or OpenTofu).

---

## 🔧 Week 2 — Security & IAM *(reconstructed — verify with your Ch 5)*

### IAM basics

- **IAM user** — identity for a person/application with long-term credentials (username + password, or access keys). **Root user** is the account owner; ⚠️ **never use root** for daily work (the AWS CLI notes repeat this).
- **Group** — collection of IAM users; attach policies to the group instead of each user.
- **Role** — identity you *assume* to get **temporary** credentials (used by services/EC2, not tied to one person).
- **Policy** — JSON document that defines **permissions** (allow/deny actions on resources).

### Authentication vs authorization

- **Authentication** = proving *who* you are (password, MFA, access key).
- **Authorization** = what you're *allowed to do* (policies).
- **MFA** = multi-factor authentication (second factor).
- **Least privilege** = grant only the minimum permissions needed.

### Shared Responsibility Model

- **AWS is responsible for** *security of the cloud* (physical data centers, hypervisor, hardware).
- **Customer is responsible for** *security in the cloud* (IAM config, data, OS patching, security groups).
- ⚠️ This is a classic exam question: "who patches the guest OS?" → **you**; "who secures the physical datacenter?" → **AWS**.

### AWS Budgeting 🔧

- Set **budgets** and **alerts** to track/monitor spend and avoid surprise bills (mentioned in Week 2 "Getting started with AWS").
- ⚠️ A budget **alerts** on spend; it does not automatically *stop* resources unless you configure budget actions.

### Security groups & NACLs (first look — full detail in Week 4)

- **Security group** — **stateful** virtual firewall at the **instance** level.
- **NACL** — **stateless** firewall at the **subnet** level.
- (Full comparison table in Week 4.)

---

## 🟠 Week 3 — Compute / EC2

### EC2 concepts

- **AMI (Amazon Machine Image)** — preconfigured template containing the OS + software for an instance.
- **Instance type** — CPU/memory/storage/network/graphics configuration.
- **Key pair** — AWS stores the **public** key, **you** store the **private** key (secure login). ⚠️ Private key lost = can't recover; you must replace it.
- **Security group** — virtual firewall specifying protocol/port/source that can reach the instance.

### EBS vs Instance store

| Feature | EBS volume | Instance store volume |
|---|---|---|
| Persistence | **persistent** (survives stop/terminate if configured) | **ephemeral** — deleted on stop/hibernate/**terminate** |
| Attachment | network-attached | physically attached to host |

⚠️ **Trap:** instance store data is **gone** when you stop, hibernate, or terminate. EBS persists.

### Elastic IP vs auto-assigned public IP

| Feature | Elastic IP | Auto-assigned public IP |
|---|---|---|
| Lifetime | yours until you **release** it | lost on stop/terminate |
| Reassignment | can remap to another instance | **cannot** be reassigned |
| Purpose | mask failures, stable DNS | simple internet access |

⚠️ **Trap:** an auto-assigned public IP **cannot be reassigned**; when the instance stops/terminates you lose it. An **Elastic IP** is a static public IPv4 that you can rapidly remap.

### Pricing models 🔧

| Model | Use case |
|---|---|
| **On-Demand** | pay per second/hour, no commitment |
| **Reserved** | commitment (1–3 yr) for discount |
| **Spot** | up to ~90% off, but **can be interrupted** |

⚠️ **Trap:** Spot instances can be **terminated** by AWS when capacity is needed → don't run stateful, non-interruptible workloads on Spot.

### SSH (lab) 🚩

```bash
# Generate a key pair (creates .ssh/aws  private + .ssh/aws.pub public)
ssh-keygen -f .ssh/aws -C "aws lab key"

# Connect to a server (admin is the default user on AWS Debian AMIs)
ssh -i .ssh/aws admin@<ip-address>

# Remove a host from ~/.ssh/known_hosts (after a re-image, host key changed)
ssh-keygen -R <host>
```

Line by line:
- `ssh-keygen -f .ssh/aws` → write keys with that path/name; `-C` adds a comment. ⚠️ `.ssh` must already exist.
- `ssh -i .ssh/aws admin@<ip>` → `-i` selects the **private** key; `admin` is the default user on AWS **Debian** AMIs.
- `ssh-keygen -R <host>` → deletes the host's entry from `known_hosts` (use after reinstalling a server so you don't get a "REMOTE HOST IDENTIFICATION HAS CHANGED" error).

### cloud-init (lab) 🚩

cloud-init is the **industry-standard, multi-distribution** instance-initialization tool; it's installed & running on default cloud images. You pass it a **Bash script or YAML** (`user-data`) to configure the image on first boot.

**Completed starter file (as the lab asks):**

```yaml
#cloud-config

users:
  - name: web
    shell: /bin/bash
    ssh_authorized_keys:
      - "ssh-ed25519 AAAAC3NzaC1... your-public-key"

packages:
  - nginx

write_files:
  - path: /var/www/html/index.html
    owner: web:web
    permissions: '0644'
    content: |
      <!DOCTYPE html>
      <html lang="en">
      <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Hello from nginx</title>
      </head>
      <body>
        <h1>Hello from nginx!</h1>
        <p>This page is being served by nginx on Debian 13.</p>
      </body>
      </html>

runcmd:
  - mkdir -p /var/www/html
  - chown -R web:web /var/www/html
  - chmod 0755 /var/www
  - chmod 0755 /var/www/html
  - systemctl enable nginx
  - systemctl restart nginx
```

Line by line:
- `#cloud-config` → first line tells cloud-init this is YAML config (not a shell script).
- `users:` → creates user `web` with bash shell and injects your **public** key into `~/.ssh/authorized_keys` (so you can SSH in).
- `packages: [nginx]` → apt-installs nginx.
- `write_files:` → writes `/var/www/html/index.html` owned by `web:web`, mode `0644`, with the HTML content. ⚠️ **`permissions: '0644'` stays quoted** (leading zero).
- `runcmd:` → shell commands run at end of boot: create the web dir, fix ownership/permissions, **enable nginx at boot**, restart it.

**Troubleshooting + test:**
```bash
cloud-init status --long   # diagnose (most errors are YAML formatting)
curl http://52.89.72.172   # test the web server (replace IP)
```

⚠️ Most cloud-init failures are **YAML formatting errors** (indentation, missing quotes). `cloud-init status --long` shows which module failed.

---

## 🔴 Week 4 — VPC & Networking (deep)

### What a VPC is

A **Virtual Private Cloud** is a **logically isolated virtual network** inside AWS. You build your own private network inside the public internet — useful for adding **security** (e.g., put a database in a subnet with **no public internet access**). A VPC exists at the **region** level (`us-west-2`). ⚠️ A **non-default VPC is fully isolated** from everything (even other VPCs) unless you explicitly connect it.

### Default vs non-default VPC

| Feature | Default VPC | Non-default VPC |
|---|---|---|
| Created | automatically, **one per region** | you create |
| CIDR | `172.31.0.0/16` | you choose `/16`–`/28` |
| Internet access | preconfigured (default route to IGW) | you must add IGW + route |
| Subnets | one **default subnet per AZ** | you create |

### CIDR (Classless Inter-Domain Routing) 🚩

An IP address has two parts: **network address** (the network's ID) and **host address** (the device on that network). CIDR notation `192.168.0.0/24` = IP + `/prefix`, where the **prefix is the number of network bits**.

- `/24` → 24 network bits + 8 host bits → **256** addresses (**254 usable**, minus network + broadcast).
- `/30` → 30 network + 2 host → 4 addresses (2 usable).
- **Smaller prefix number = bigger address space.** `/16` = 65,536; `/28` = 16.

**Classful (old) vs classless (CIDR):**

| Class | Network bits | Hosts |
|---|---|---|
| A | 8 | 16,777,214 |
| B | 16 | 65,534 |
| C | 24 | 254 |

Classful addressing **wasted addresses** (an org needing 300 hosts got a class B of 65,534 and wasted 65,234) and couldn't **combine** class-C networks. **CIDR/VLSM** fixes this by making network/host split flexible.

**RFC 1918 private ranges (use for VPC):**

| Range | CIDR | Example VPC block |
|---|---|---|
| 10.0.0.0 – 10.255.255.255 | 10/8 | 10.0.0.0/16 |
| 172.16.0.0 – 172.31.255.255 | 172.16/12 | 172.31.0.0/16 |
| 192.168.0.0 – 192.168.255.255 | 192.168/16 | 192.168.0.0/20 |

⚠️ **VPC CIDR limits:** must be between **`/16` (max, 65,536 IPs)** and **`/28` (min, 16 IPs)**. **Blocked ranges you cannot use:** `0.0.0.0/8`, `127.0.0.0/8` (loopback), `169.254.0.0/16` (link-local), `224.0.0.0/4` (multicast).

**Subnetting math (4 moves):**
1. Convert prefix to mask: `/26` → `255.255.255.192`.
2. **Block size** = `256 − last-octet` → `256 − 192 = 64`.
3. List subnet starts: `0, 64, 128, 192`.
4. **Usable hosts = block size − 2** (e.g. `/26` → 62).

**Worked example:** split `172.16.0.0/16` into ≥10 equal subnets → need 4 extra bits (`2⁴=16` ≥ 10) → new prefix **`/20`**, each holds **4094 hosts**, ranges `172.16.0.0`, `172.16.16.0`, `172.16.32.0` … `172.16.240.0`.

**Supernet:** combine adjacent nets, e.g. `192.168.0.0/23` = `192.168.0.0` + `192.168.1.0` (mask `255.255.254.0`) → **one** routing entry instead of two.

### Subnets

- A VPC must contain **≥1 subnet**; each subnet is a **CIDR subset of the VPC CIDR** and lives in **exactly one AZ**.
- A subnet can't span AZs; a VPC spans the whole region and can contain subnets in multiple AZs.
- **Public subnet** = has a route to an **internet gateway** (default route `0.0.0.0/0` → IGW). **Private subnet** = no IGW route.

### Route tables

- Every VPC gets a **default (main) route table** automatically.
- A route maps a destination CIDR to a **target**. `0.0.0.0/0` = "all other traffic" (the **default route**).
- Subnets are associated with route tables (explicitly or the main table). ⚠️ The lab associates `bcit-demo-rt` with the **private** subnet, then adds `0.0.0.0/0 → IGW` to the **main** table — so the **public** subnet (still on main) gets internet, the private subnet doesn't.

### Internet gateway (IGW) & NAT

- **Internet gateway** — attach to a VPC; enables public IP + internet access. A subnet is **public** only if its route table has a route to an attached IGW **and** instances have public IPs.
- **NAT (gateway)** — lets **private** subnets reach the internet (e.g., to download updates) **without** being reachable *from* the internet (outbound-only). ⚠️ **Not used in the lab**, but exam-relevant: NAT = outbound internet for private instances.

### Security Groups vs NACLs 🚩 (stateless vs stateful — core!)

| Feature | **Security Group** | **NACL** |
|---|---|---|
| Operates at | **instance** (ENI) level | **subnet** level |
| **State** | **Stateful** | **Stateless** |
| Default rules | **no inbound** (deny all), **all outbound** | **allow all** in & out |
| Rule types | **allow only** (no deny rules) | **allow AND deny** |
| Rule evaluation | all rules evaluated (most permissive) | rules evaluated **in order (lowest number first)** |
| Return traffic | **automatically allowed** | **must be explicitly allowed** (ephemeral ports) |

⚠️ **The #1 stateless/stateful fact for this exam:**
- A **security group is stateful** — if you allow outbound HTTP, the **response is automatically allowed back in** regardless of inbound rules. You never write a "return traffic" rule.
- A **NACL is stateless** — it tracks **no connection state**, so you must **explicitly allow both directions** (including the **ephemeral port range 1024–65535** for the return traffic).

### DNS hostnames / auto-assign public IP (from the lab walkthrough)

- **Enable DNS hostnames** on the VPC → instances get DNS names.
- **Enable auto-assign public IPv4** on the **public** subnet → instances launched there automatically get a public IP.

### VPC connectivity options (Ch 10)

| Option | What it connects | Notes |
|---|---|---|
| **VPC peering** | 2 VPCs (private, point-to-point) | same or different region; no internet needed |
| **VPN** | VPC ↔ on-prem/office over **public internet** | virtual private gateway + customer gateway; **AES 128/256**; BGP or static; ≤10 per VPC |
| **Direct Connect** | VPC ↔ on-prem via **dedicated private line** | 1 or 10 Gbps; hosted 50–500 Mbps; **no internet**, low/predictable latency, more expensive |

⚠️ **Trap:** Direct Connect **does not provide internet access** (separate circuit needed). VPN uses the **internet**; Direct Connect bypasses it. Peering = exactly **two** VPCs, private.

*(Out of scope per README — skim only: Route 53 DNS/registrar/routing policies, CloudFront CDN/edge locations.)*

---

## 🟠 Week 5 — AWS CLI + Bash scripting (deep)

### Install & versions

- **v1 vs v2:** both use the top-level command `aws`; you're using **v2**. ⚠️ Distro package repos often ship **v1** — check you're installing v2 (current ≈ 2.37.4).
- Manual install: `curl -fsSL https://awscli.amazonaws.com/v2/install.sh | bash` → installs to `$HOME/.local/bin` (add to PATH if needed). Verify: `aws --version`.
- Optional completion: `complete -C aws_completer aws`.

### Auth & config

- Config lives in **`~/.aws`** (INI-style), split into **profiles** (separate credentials per account/activity; default profile if you don't need separation).
- **`aws login`** → browser login as your **IAM user** (not root), prompts for region (set `us-west-2`), stored in `~/.aws/config`, creates **short-term credentials**. **`aws login --remote`** if you're inside a VM.
- ⚠️ Next `aws login` just creates fresh short-term credentials — no reconfig. Downside: still browser login. (Long-term creds / Identity Center = later.)

### Command structure

```
aws <service> <subcommand> [options]
# base  top-level  operation     options
aws  ec2         describe-key-pairs --output text
```

- Top-level ≈ a service (`ec2`); subcommand ≈ an operation (`create-key-pair`, `import-key-pair`, `delete-key-pair`, `describe-key-pairs`, `describe-images`).
- ⚠️ Subcommand names mirror the **web console** language.

### `--query` (JMESPath) + `--output`

```bash
# print all key names as plain text (default output is JSON)
aws ec2 describe-key-pairs --query 'KeyPairs[*].KeyName' --output text

# newest key name using sort_by + last element
aws ec2 describe-key-pairs \
  --query 'KeyPairs | sort_by(@, &CreateTime) | [-1].KeyName' \
  --output text

# get the KeyPairId of a specific key
aws ec2 describe-key-pairs \
  --key-names "bcit-demo" \
  --query 'KeyPairs[0].KeyPairId' \
  --output text
```

Sample `--output yaml` result for `describe-key-pairs`:
```yaml
KeyPairs:
- CreateTime: '2026-09-20T22:28:04.792000+00:00'
  KeyFingerprint: XJxIQX+JEMBZNlq3TIdtrcp0twH4onuYL+5BVSuALCI=
  KeyName: bcit-demo
  KeyPairId: key-03ae06856396559ae
  KeyType: ed25519
  Tags: []
```

JMESPath cheat: `[*]` = all elements; `[0]` / `[-1]` = first/last; `sort_by(@, &field)` = sort; `|` = pipe result into next expression. `--output text|yaml|json`.

### Key pair operations

```bash
aws ec2 delete-key-pair --key-name "bcit-demo"
# returns:
# { "Return": true, "KeyPairId": "key-03ae06856396559ae" }

aws ec2 import-key-pair --key-name "bcit-demo" --public-key-material fileb://~/.ssh/aws.pub
```

### `file://` vs `fileb://` 🚩

| Prefix | Behavior |
|---|---|
| `file://` | reads file + applies normal CLI **parameter encoding** |
| `fileb://` | reads file as **raw binary**, no encoding |

⚠️ For SSH public keys use **`fileb://`** (raw bytes, no mangling).

### Full Bash script 1 — import a key (from source)

```bash
#!/usr/bin/env bash
set -euo pipefail

# Function to handle errors
err() {
  local error_message="$*"
  echo -e "\033[1;31m ERROR:\033[0m ${error_message}" >&2
  exit 1
}

# Define variables
key_name="bcitkey"
public_key_file=""

# Check arguments
if [[ $# -ne 1 ]]; then
  err "Script requires the path to the public key file you would like to import."
fi

# Check if the public key file is a regular file
if [[ ! -f "$1" ]]; then
  err "Path to public key for import is incorrect; file does not exist."
else
  public_key_file="$1"
fi

# Check if key already exists to prevent duplicate errors
if aws ec2 describe-key-pairs --key-names "$key_name" &>/dev/null; then
  err "Key pair '$key_name' already exists in AWS. Delete it first or use a different name."
fi

echo "Importing public key into AWS account..."
aws ec2 import-key-pair \
  --key-name "$key_name" \
  --public-key-material fileb://"$public_key_file" > key_data

echo "Key imported successfully. Details saved to 'key_data'."
```

Line by line:
- `#!/usr/bin/env bash` → shebang; run with bash found via PATH.
- `set -euo pipefail` → `-e` exit on any command error; `-u` error on unset variable; `-o pipefail` fail if *any* command in a pipeline fails.
- `err() { local error_message="$*" ... }` → function; `$*` = all args; `local` scopes the var; `\033[1;31m` = red bold ANSI, `\033[0m` reset; `>&2` writes to **stderr**; `exit 1` = non-zero (failure) exit.
- `key_name="bcitkey"`, `public_key_file=""` → initialize variables.
- `if [[ $# -ne 1 ]]` → `$#` = argument count; requires exactly 1.
- `[[ ! -f "$1" ]]` → `-f` true if file exists; `!` negates; else branch stores `$1` in `public_key_file`.
- `if aws ... &>/dev/null` → run describe; `&>/dev/null` discards both stdout+stderr; the `if` treats a **successful** describe (key exists) as true → error out (prevent duplicate).
- `> key_data` → redirect import **stdout** to a file named `key_data`.

**Run it:** `./script ~/.ssh/aws` (or `bash script ~/.ssh/aws.pub`).

### Full Bash script 2 — get latest Debian AMI (the CLI lab task)

The task: take `describe-images` output, keep **only the most recent single ImageId**, store it via **command substitution**, write it with a **heredoc**.

```bash
#!/usr/bin/env bash
set -euo pipefail

# store the single newest Debian 13 amd64 free-tier AMI ID
ami_id=$(aws ec2 describe-images \
  --owners 136693071363 \
  --filters \
    "Name=name,Values=debian-13-amd64-*" \
    "Name=architecture,Values=x86_64" \
    "Name=root-device-type,Values=ebs" \
    "Name=free-tier-eligible,Values=true" \
  --query 'sort_by(Images, &CreationDate)[-1].ImageId' \
  --output text)

# write it out in sourceable "name=value" form
cat > ami.txt <<EOF
debian_ami=${ami_id}
EOF

echo "Saved:"
cat ami.txt
```

**Sample output:**
```
Saved:
debian_ami=ami-0b3c68efb8f9567ef
```

Line by line:
- `ami_id=$( ... )` → **command substitution**: run the command, capture stdout into `ami_id`.
- `--owners 136693071363` → Debian's AWS account ID (verify by hand via Debian wiki; better than guessing).
- `--filters "Name=...,Values=..."` → narrow by image name pattern, architecture `x86_64`, root device `ebs`, free-tier eligible.
- `--query 'sort_by(Images, &CreationDate)[-1].ImageId'` → sort by creation date ascending, take **last** (`[-1]`) = newest, return only `.ImageId`.
- `cat > ami.txt <<EOF` → **heredoc**: feed everything until `EOF` as stdin to `cat`, redirected to `ami.txt`.
- `debian_ami=${ami_id}` → expands the variable → produces a `name=value` line you could later `source ami.txt`.

⚠️ **Trap:** the original task's `--query` used `[*].[ImageId,Name,CreationDate]` (returns ALL, with name + date). To satisfy "only the most recent AMI ID, just a single ID," you must change the query to `sort_by(...)[-1].ImageId` — not just filter the output text.

### Bash quick-reference (exam-relevant)

| Construct | Meaning |
|---|---|
| `#!/usr/bin/env bash` | portable shebang |
| `set -euo pipefail` | strict mode |
| `$#` `$1` `$*` `$@` | arg count, 1st arg, all args |
| `$(command)` | command substitution |
| `cat > f <<EOF ... EOF` | heredoc |
| `[[ -f f ]]` `[[ -z s ]]` `[[ $# -ne 1 ]]` | file exists / empty / not equal |
| `&&` `\|\|` | AND / OR short-circuit |
| `>&2` | write to stderr |
| `&>/dev/null` | discard stdout+stderr |
| `exit 1` | fail exit code |
| `local` | function-local variable |

---

## 🟠 Labs

### W1 lab — Linux environment

Three ways: **switch to Linux** (or `distrobox` to isolate), **VirtualBox VM** (headless OK), or **WSL**.

⚠️ **WSL filesystem gotcha:** WSL creates its **own filesystem**. Working from the **Windows** filesystem (path shows `/mnt/c`) causes **permission errors** and is slower. Tell you're in Windows FS when the prompt shows `/mnt/c`. Fix: run `cd` alone (returns home) or configure WSL to start in your Linux home. `explorer.exe .` opens Windows Explorer in the current dir. Optional: enable systemd in `/etc/wsl.conf` (`[boot] systemd=true`).

### W3 lab — EC2 + cloud-init nginx (see Week 3 section above)

### W4 lab — build a VPC (walkthrough; internalize the order!)

1. **VPC** `bcit-demo-vpc`, CIDR `10.0.0.0/16` → enable **DNS hostnames**.
2. **Subnets:** `bcit-demo-sub-pb` (AZ `us-west-2a`, `10.0.1.0/24`) → enable **auto-assign public IPv4**; `bcit-demo-sub-pr` (AZ `us-west-2b`, `10.0.2.0/24`).
3. **Route table** `bcit-demo-rt` → associate with the **private** subnet.
4. **Internet gateway** `bcit-demo-igw` → **attach to VPC**.
5. **Main route table** → add route `0.0.0.0/0` → **IGW** (this is what makes the *public* subnet public).
6. **Launch:** public EC2 `bcit-demo-pb` (Debian) into the public subnet, SG allows **SSH** from anywhere; private EC2 `bcit-demo-pr` into the private subnet, SG allows **ICMP** from anywhere.

⚠️ **Why it works:** public subnet uses the **main** RT (has `0.0.0.0/0 → IGW`) → internet. Private subnet uses `bcit-demo-rt` (no IGW route) → stays private. ⚠️ **No NAT** → the private instance can't reach the internet itself; it only needs **ICMP** (ping) from the public instance *within* the VPC.

### W5 lab — CLI (see Week 5 scripts above)

---

## 🚩 Cross-cutting: Stateless vs Stateful (the 2 written questions)

### 1. Network statelessness (HTTP)

**Stateless** protocol = each **request is independent**; the server keeps **no memory** of previous requests from the client. **HTTP is stateless**: every request carries everything needed to be understood (method, headers, body); the server doesn't remember "this client logged in earlier."

- Contrast **stateful**: a connection or session where the server *remembers* state (e.g., a logged-in session, a persistent TCP connection, a stateful firewall tracking the connection).
- Consequence: to simulate "state" on the web you add **cookies/tokens** on the client side — the server stays stateless.
- ⚠️ Don't confuse "HTTP is stateless" with "TCP is connection-oriented": TCP (transport) is connection-oriented; HTTP (application) is stateless *on top* of it.

### 2. VPC statelessness (NACL vs Security Group)

- **Security group = stateful.** It **remembers** the connection: allow outbound → **reply automatically allowed back in** (no explicit return rule, no ephemeral-port rule needed).
- **NACL = stateless.** It **tracks no connection**. Both directions must be **explicitly allowed**, including the **ephemeral port range (1024–65535)** for the return path, or the response is dropped.

⚠️ **The classic trap:** "I added an inbound NACL rule for SSH (port 22) but SSH still fails." Because the **outbound** (return) rule for the ephemeral port is missing — NACLs are **stateless**. With a **security group**, allowing inbound SSH is enough (stateful).

---

# Part 3 — Practice test (mirrors the real format, "hard" difficulty)

## Section A — 20 "select all that apply" (A–F)

**A1.** Which statements are TRUE about a **default VPC**? (Select all that apply.)
A. AWS creates a default VPC in each Region.
B. A default VPC spans multiple Regions.
C. AWS creates a default VPC in each Availability Zone.
D. A default VPC's CIDR is 172.31.0.0/16.
E. A default VPC is preconfigured to allow instances to reach the internet.
F. A default VPC contains one default subnet in every Availability Zone.

**A2.** Which of the following are VALID CIDR blocks for an AWS VPC? (Select all that apply.)
A. 10.0.0.0/16
B. 10.0.0.0/8
C. 10.0.0.0/28
D. 10.0.0.0/29
E. 172.31.0.0/16
F. 192.168.0.0/24

**A3.** Which CIDR blocks are **NOT allowed** for a VPC? (Select all that apply.)
A. 0.0.0.0/8
B. 127.0.0.0/8
C. 10.0.0.0/16
D. 169.254.0.0/16
E. 224.0.0.0/4
F. 192.168.0.0/24

**A4.** Which are TRUE about **subnets**? (Select all that apply.)
A. A subnet's CIDR must be a subset of its VPC's CIDR.
B. A subnet spans multiple Availability Zones.
C. A subnet exists within exactly one Availability Zone.
D. A subnet with a route to an internet gateway is a public subnet.
E. Every VPC must contain at least two subnets.
F. A subnet can have a CIDR of /29 if the VPC is /16.

**A5.** Which are TRUE about a **new security group** (no edits made)? (Select all that apply.)
A. It has no inbound rules, so no unsolicited inbound traffic is allowed.
B. It contains an inbound rule allowing all traffic by default.
C. It contains an outbound rule allowing access to any IP address.
D. It contains an outbound rule denying all traffic by default.
E. It is stateless.
F. It can be attached to EC2 instances.

**A6.** A security group allows inbound SSH (TCP 22). You SSH in and get a response. Which explain why this works? (Select all that apply.)
A. Security groups are stateful, so reply traffic is automatically allowed.
B. You also need an explicit outbound rule for the SSH reply.
C. You need an ephemeral-port inbound rule for the reply.
D. NACLs are stateless, so the reply must be explicitly allowed — but that applies at the subnet level.
E. The outbound "allow all" rule permits the reply.
F. SSH is a stateless protocol, so no return rule is needed.

**A7.** Which are TRUE about **NACLs** (network ACLs)? (Select all that apply.)
A. A NACL operates at the subnet level.
B. A NACL operates at the instance level.
C. A NACL is stateless.
D. A NACL's default NACL allows all traffic in and out.
E. A NACL can deny traffic, unlike a security group.
F. A NACL's rules are evaluated starting from the lowest rule number.

**A8.** Which correctly pair a firewall with its state behavior? (Select all that apply.)
A. Security group — stateful
B. Security group — stateless
C. NACL — stateful
D. NACL — stateless
E. Security group — allows return traffic automatically
F. NACL — allows return traffic automatically

**A9.** Which are TRUE about **Elastic IP addresses**? (Select all that apply.)
A. An Elastic IP is a static IPv4 address.
B. It can be remapped to another instance.
C. An automatically-assigned public IP is lost when the instance stops.
D. An Elastic IP persists until you release it.
E. An automatically-assigned public IP can be reassigned to a different instance.
F. An Elastic IP is a private IPv4 address only.

**A10.** Which are TRUE about **EBS vs instance store**? (Select all that apply.)
A. EBS volumes are persistent.
B. Instance store data survives a terminate.
C. Instance store data is lost on stop, hibernate, or terminate.
D. EBS is physically attached to the host.
E. Instance store is ephemeral.
F. EBS volumes can't be detached and reattached.

**A11.** Which are TRUE about **VPC peering**? (Select all that apply.)
A. It is a private point-to-point connection between two VPCs.
B. It requires internet access on both VPCs.
C. It connects more than two VPCs in a mesh by default.
D. It can connect VPCs in different Regions.
E. It traverses the public internet.
F. It is a VPN connection.

**A12.** Which are TRUE about **VPN vs Direct Connect**? (Select all that apply.)
A. A VPN traverses the public internet.
B. Direct Connect provides predictable, low latency.
C. Direct Connect provides internet access.
D. VPN connections use AES 128- or 256-bit encryption.
E. Direct Connect is a dedicated private link (1 or 10 Gbps).
F. Direct Connect is always cheaper than a VPN.

**A13.** Which are TRUE about **IAM**? (Select all that apply.)
A. A role provides temporary credentials.
B. The root user should be used for daily tasks.
C. A policy is a JSON document defining permissions.
D. A group is a collection of IAM users.
E. MFA adds a second factor of authentication.
F. Least privilege means granting maximum permissions.

**A14.** Which are TRUE about the **AWS CLI**? (Select all that apply.)
A. `aws` is the top-level command for both v1 and v2.
B. `aws login` should be run as the root user.
C. Configuration is stored in ~/.aws in INI format.
D. Profiles allow separate credentials for different accounts.
E. The default output of describe-key-pairs is YAML.
F. `fileb://` reads a file as raw binary.

**A15.** Which describe how to get the **single newest** Debian AMI ImageId with the CLI? (Select all that apply.)
A. Use `--query 'sort_by(Images, &CreationDate)[-1].ImageId'`.
B. Use `--query 'sort_by(Images, &CreationDate)[0].ImageId'`.
C. Use `--output text` to get a bare value.
D. Use `--filters` to restrict name/architecture/free-tier.
E. Use `--owners` set to your own account ID.
F. Store the result with command substitution `$( ... )`.

**A16.** In the script `set -euo pipefail`, what do the flags do? (Select all that apply.)
A. `-e` exits the script on any command error.
B. `-u` errors on unset variables.
C. `-o pipefail` makes a pipeline fail if any command in it fails.
D. `-e` ignores all errors.
E. `-u` makes variables global.
F. `-o pipefail` redirects all output to stderr.

**A17.** Which are TRUE about **cloud-init**? (Select all that apply.)
A. It uses `#cloud-config` to signal YAML config.
B. `packages:` installs software like nginx.
C. `write_files:` writes files with specified owner/permissions.
D. `runcmd:` commands run at the very start of boot, before networking.
E. It is an industry-standard multi-distribution instance-init tool.
F. `cloud-init status --long` helps diagnose failures.

**A18.** Which are TRUE about the **Linux/WSL** setup? (Select all that apply.)
A. Working from `/mnt/c` (Windows filesystem) can cause permission errors.
B. WSL shares the same filesystem as Windows.
C. `cd` alone returns you to your WSL home directory.
D. `explorer.exe .` opens Windows Explorer in the current directory.
E. WSL creates its own filesystem separate from Windows.
F. systemd cannot be enabled in WSL 2.

**A19.** Which are TRUE about **cloud deployment/service models**? (Select all that apply.)
A. AWS is a public cloud.
B. AWS + on-premises = hybrid cloud.
C. EC2 is an example of IaaS.
D. Vercel is an example of SaaS.
E. Google Docs is an example of SaaS.
F. On-premises always means private cloud.

**A20.** Which are TRUE about **regions and Availability Zones**? (Select all that apply.)
A. A Region contains multiple Availability Zones.
B. Each AWS Region has at least three Availability Zones.
C. A VPC spans a single Availability Zone.
D. A subnet lives in a single Availability Zone.
E. `us-west-2a` and `us-west-2b` are Availability Zones.
F. An Availability Zone spans multiple Regions.

---

## Section B — 10 short-answer

**B1.** What is the range of allowed IPv4 CIDR block sizes for a VPC (in prefix notation), and how many addresses do the two endpoints hold?

**B2.** List the three RFC 1918 private address ranges (CIDR notation).

**B3.** Name four CIDR ranges that AWS forbids you to assign to a VPC.

**B4.** What is the single most important difference between a security group and a NACL with respect to *return traffic*, and why does it matter when you allow SSH?

**B5.** In `aws ec2 <subcommand>`, what are the three structural parts of the command called, and what does the subcommand generally correspond to?

**B6.** What does `fileb://` do differently from `file://`, and which would you use for an SSH public key?

**B7.** Explain what `set -euo pipefail` does (one line per flag).

**B8.** What does `$#` and `$1` mean in a Bash script?

**B9.** In the VPC lab, why is `bcit-demo-sub-pb` public while `bcit-demo-sub-pr` is private? (Reference the route table and IGW.)

**B10.** Why does "enable auto-assign public IPv4 address" matter on a public subnet, and where do you enable it?

---

## Section C — Written response

**C1 (VPC design).** You are given VPC `10.0.0.0/16` in `us-west-2`. Design a two-tier setup: a public web subnet and a private database subnet.
- (a) Choose subnets (AZs + CIDRs) and justify why your CIDRs are valid subsets.
- (b) Explain exactly which resources you create and the exact routes/associations that make one subnet public and the other private.
- (c) Explain how the database gets software updates without being reachable from the internet, and name the resource that enables this.
- (d) Explain what a security group vs a NACL should each allow/deny for SSH to the web server, and why one of them requires extra rules for return traffic.

**C2 (Bash scripting).** Write a complete Bash script that:
- takes a key name and a public key path as arguments,
- validates the file exists,
- checks whether the key already exists in AWS,
- imports the key with `fileb://`,
- prints a red error and exits 1 on any failure.
Then show the exact command to run it and give sample success + failure output.

**C3 (Stateless — network).** Explain what it means for HTTP to be a *stateless* protocol. Contrast it with a *stateful* interaction, and explain how web applications simulate state despite HTTP being stateless.

**C4 (Stateless — VPC).** A developer opens SSH (TCP 22) inbound in a security group and SSH works. Then they replace the security group with a NACL that allows TCP 22 inbound, and SSH breaks. Explain precisely why, using the terms *stateful*, *stateless*, and *ephemeral ports*, and state what rule they must add to fix it.

---

## Answer key

### Section A

**A1 → A, D, E, F.**
- A ✔ (default VPC is per-Region).
- B ✘ (a VPC never spans Regions).
- C ✘ (AWS creates a default **subnet**, not VPC, in each AZ).
- D ✔ (172.31.0.0/16 is the default VPC CIDR).
- E ✔ (default VPC is preconfigured for internet via IGW).
- F ✔ (one default subnet per AZ).

**A2 → A, C, E, F.**
- A ✔ (/16 allowed). B ✘ (/8 is larger than the /16 max). C ✔ (/28 allowed — the minimum). D ✘ (/29 is smaller than the /28 minimum). E ✔. F ✔ (/24 is within /16–/28).

**A3 → A, B, D, E.**
- A ✔ (0.0.0.0/8 blocked). B ✔ (loopback blocked). C ✘ (valid). D ✔ (link-local blocked). E ✔ (multicast blocked). F ✘ (valid private range).

**A4 → A, C, D.**
- A ✔. B ✘ (subnet is single-AZ). C ✔. D ✔ (route to IGW = public). E ✘ (needs ≥1, not ≥2). F ✘ (subnet CIDR must also be /16–/28; /29 invalid).

**A5 → A, C, F.**
- A ✔ (no inbound rules by default). B ✘ (no inbound rules by default). C ✔ (default outbound allow-all). D ✘ (outbound is allow, not deny). E ✘ (security groups are stateful). F ✔.

**A6 → A, D.**
- A ✔ (stateful → reply auto-allowed). B ✘ (no explicit return rule needed for SG). C ✘ (no ephemeral rule needed for SG). D ✔ (true statement about NACLs, even though SG is what's in use). E ✘ (the outbound allow-all exists, but the *reason* reply works is statefulness — this is the trap). F ✘ (SSH is a stateful/connection-oriented interaction; "stateless protocol" is wrong).

**A7 → A, C, D, E, F.**
- A ✔. B ✘ (NACL is subnet-level; SG is instance-level). C ✔. D ✔ (default NACL allows all). E ✔ (NACLs support deny). F ✔ (rules evaluated lowest-number first).

**A8 → A, D, E.**
- A ✔. B ✘. C ✘. D ✔. E ✔ (SG auto-allows return). F ✘ (NACL does not auto-allow return).

**A9 → A, B, C, D.**
- A ✔. B ✔ (remap = the point of EIP). C ✔. D ✔. E ✘ (auto-assigned public IPs **cannot** be reassigned). F ✘ (EIP is a **public** IPv4).

**A10 → A, C, E.**
- A ✔. B ✘ (instance store is lost on terminate). C ✔. D ✘ (EBS is network-attached; instance store is physically attached). E ✔. F ✘ (EBS can be detached/reattached).

**A11 → A, D.**
- A ✔. B ✘ (peering needs no internet). C ✘ (exactly two VPCs). D ✔ (same or different Region). E ✘ (private AWS network, not internet). F ✘ (not a VPN).

**A12 → A, B, D, E.**
- A ✔. B ✔. C ✘ (DX provides **no** internet). D ✔ (AES 128/256). E ✔. F ✘ (DX is generally **more** expensive).

**A13 → A, C, D, E.**
- A ✔. B ✘ (never use root daily). C ✔. D ✔. E ✔. F ✘ (least privilege = minimum).

**A14 → A, C, D, F.**
- A ✔. B ✘ (never root). C ✔. D ✔. E ✘ (default is JSON; YAML only if `--output yaml`). F ✔.

**A15 → A, C, D, F.**
- A ✔ (`[-1]` = newest). B ✘ (`[0]` = oldest). C ✔. D ✔. E ✘ (owners = **Debian's** account 136693071363, not yours). F ✔.

**A16 → A, B, C.**
- A ✔. B ✔. C ✔. D ✘. E ✘ (`-u` does not make vars global). F ✘ (pipefail has nothing to do with stderr).

**A17 → A, B, C, E, F.**
- A ✔. B ✔. C ✔. D ✘ (`runcmd` runs near the **end** of boot, not before networking). E ✔. F ✔.

**A18 → A, C, D, E.**
- A ✔. B ✘ (WSL has its **own** filesystem). C ✔. D ✔. E ✔. F ✘ (systemd can be enabled via /etc/wsl.conf).

**A19 → A, B, C, E.**
- A ✔. B ✔. C ✔ (IaaS). D ✘ (Vercel is **PaaS**). E ✔. F ✘ (on-prem ≠ private cloud).

**A20 → A, B, D, E.**
- A ✔. B ✔. C ✘ (a VPC spans the whole Region). D ✔. E ✔. F ✘ (an AZ is within a Region, not across).

### Section B

**B1.** Between **/16** and **/28**. /16 = **65,536** addresses; /28 = **16** addresses.

**B2.** `10.0.0.0/8`; `172.16.0.0/12` (172.16.0.0–172.31.255.255); `192.168.0.0/16`.

**B3.** `0.0.0.0/8`; `127.0.0.0/8` (loopback); `169.254.0.0/16` (link-local); `224.0.0.0/4` (multicast).

**B4.** A security group is **stateful** (return traffic auto-allowed), a NACL is **stateless** (return must be explicitly allowed). With SSH: a SG needs only the inbound 22 rule; a NACL needs inbound 22 **plus** outbound ephemeral ports (1024–65535) or the reply is dropped.

**B5.** `aws` (base) · `ec2` (top-level/service) · `describe-key-pairs` (subcommand/operation). The subcommand mirrors the **web console** operation name.

**B6.** `fileb://` reads raw **binary** (no encoding); `file://` applies normal parameter encoding. Use **`fileb://`** for an SSH public key.

**B7.** `-e` = exit on error; `-u` = error on unset variable; `-o pipefail` = pipeline fails if any command in it fails.

**B8.** `$#` = number of positional arguments; `$1` = the first argument.

**B9.** The public subnet uses the **main** route table, which got the route `0.0.0.0/0 → internet gateway`. The private subnet was associated with `bcit-demo-rt`, which has **no** IGW route. (The public subnet also has auto-assign public IPv4 enabled.)

**B10.** It auto-assigns a public IPv4 to instances launched in that subnet (required to reach the internet). Enabled on the **subnet** via Actions → Edit subnet settings.

### Section C (model answers)

**C1.** (a) Public web: `10.0.1.0/24` in `us-west-2a`; private DB: `10.0.2.0/24` in `us-west-2b` — both `/24` are valid because they're within `/16`–`/28` and are subsets of `10.0.0.0/16`. (b) Create IGW → attach to VPC → add `0.0.0.0/0 → IGW` to the **public** subnet's route table (or the main table the public subnet uses); associate the private subnet with a route table that has **no** IGW route; enable auto-assign public IP on the public subnet. (c) Use a **NAT gateway** placed in the public subnet: the private subnet's route table gets `0.0.0.0/0 → NAT`, giving outbound-only internet so the DB can download updates without being reachable from the internet. (d) SG on the web server: inbound TCP 22 from your IP only — **stateful**, return traffic automatic. NACL on the subnet: inbound TCP 22 **and** outbound ephemeral ports (1024–65535) because NACLs are **stateless** and need an explicit return path.

**C2.** (script) — same as the import script in Week 5, but parameterize `key_name`:

```bash
#!/usr/bin/env bash
set -euo pipefail
err() { echo -e "\033[1;31m ERROR:\033[0m $*" >&2; exit 1; }
[[ $# -ne 2 ]] && err "Usage: $0 <key-name> <public-key-file>"
key_name="$1"; key_file="$2"
[[ ! -f "$key_file" ]] && err "File does not exist: $key_file"
if aws ec2 describe-key-pairs --key-names "$key_name" &>/dev/null; then
  err "Key '$key_name' already exists."
fi
aws ec2 import-key-pair --key-name "$key_name" \
  --public-key-material "fileb://$key_file"
echo "Imported '$key_name'."
```

Run: `./import.sh mykey ~/.ssh/aws.pub`. Success output: `Imported 'mykey'.` Failure output: red `ERROR: File does not exist: /bad/path`.

**C3.** HTTP is **stateless**: each request is self-contained and independent; the server retains **no memory** between requests, so two requests from the same client are unrelated to the server. A **stateful** interaction remembers prior context (e.g., a logged-in session or a tracked TCP connection). Web apps simulate state by storing session info **client-side** (cookies/tokens) that the client resends with each request — the server remains stateless.

**C4.** The security group is **stateful**: it tracks the connection, so once inbound 22 is allowed, the **reply traffic is automatically permitted** out (no return rule needed). A **NACL is stateless**: it tracks no connection, so allowing inbound 22 alone is not enough — the **outbound** reply (destined for an **ephemeral port**, 1024–65535, on the client) is **dropped**. Fix: add an outbound NACL rule allowing TCP **1024–65535** to the client (and ensure the inbound 22 rule is evaluated first by rule number).

---

*End of guide. Cross-check the 🔧 (reconstructed) Week 2/Week 3 sections against your O'Reilly chapters. Re-take your past labs/quiz questions closed-book before this test.*
