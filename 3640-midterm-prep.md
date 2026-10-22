# 3640 Fall 2026 — Midterm Prep Guide (Weeks 1–7)

> **Midterm snapshot:** Tue Oct 27, 14:00–15:00, DTC-825, **60 minutes**, worth **30%** of final grade.
> **Scope:** everything from Weeks 1–7. Professor confirmed: **Week 7 (storage) IS included**, no single week dominates, but there is **heavy overlap** — AWS CLI (introduced W5, reused W7), recurring terminology (e.g. **"Elastic"**), and repeated material like **cloud-init**. Expect **scenario-based storage questions** ("which service is most appropriate / when to use one over the other"). Review **labs AND flipped material**.

## Color / priority legend

| Marker | Meaning |
|---|---|
| 🔴 **W4 / VPC** | Highest priority + explicit exam emphasis |
| 🟠 **W3 / W5 / W7 / Labs** | High priority |
| 🟡 **W1 / W2** | Foundational, lighter weighting |
| 🚩 | Matches reported exam emphasis (**VPC, stateless, bash, storage, Elastic, cloud-init**) |
| ⚠️ | Common mistake / exam trap / quirk |
| 🔧 | **Reconstructed** (source chapter not uploaded — verify against your O'Reilly copy) |

---

# Part 0 — Professor's guidance (verbatim intent) + source notes

From your screenshot (professor's message about the midterm):

- **Week 7 material is on the midterm.** Questions may be on **general aspects of the storage services**, or **"when you would use one over the other"** → **scenario-based** "pick the most appropriate storage service" questions.
- **No single week is focused on**; a lot of content **overlaps** — e.g. AWS CLI (W5 → reused in W7).
- **Recurring terminology** is fair game — e.g. **what "Elastic" means** (Elastic IPs, Elastic Block Store, Elastic File System…).
- **Repeated material** like **cloud-init** will likely be tested.
- **Review the labs as well as the flipped material.**

### Source errors / quirks (carried over + Week 7 notes)

1. Week 2 (Ch 5) & Week 3 (Ch 7) readings were external O'Reilly links, **not uploaded** → reconstructed 🔧.
2. `aws-vpc.md` typo "public **inernet**"; route-table naming inconsistency (IGW route actually goes on the **main** table, which the public subnet uses). **No NAT gateway** in the lab.
3. `vpc.pdf`: "the *smaller* the CIDR size, the *greater* the number of IP addresses" — ⚠️ read as: smaller prefix number (`/16`) = more addresses.
4. `aws-cli.md`: default output is **JSON**, not YAML; `aws login`/`--remote` are new v2 browser-flow commands; never root.
5. `aws-ec2.md`: `ssh-keygen -f .ssh/aws` needs `.ssh` to already exist; cloud-init `permissions "0644"` must stay quoted.
6. **Week 7 (storage):** the pasted chapter text uses **"99.99% availability … backed by an SLA"** for S3, but elsewhere lists **S3 Standard-IA at 99.9%** and **One Zone-IA at 99.5%** — don't memorize one number blindly; availability **varies by storage class**. Also note **One Zone-IA / Express One Zone store in a SINGLE AZ** (lower durability/redundancy than multi-AZ classes).

---

# Part 1 — Complete topic list (Weeks 1–7)

*(Weeks 1–5 unchanged from before; Week 7 added below.)*

## 🟡 Week 1 — Cloud fundamentals
- NIST cloud definition; consumption-based pricing; why cloud (flexibility/security/efficiency/cost)
- Components (servers/VPS, networking, storage); deployment models (public/community/private/hybrid; on-prem ≠ private)
- Service models **IaaS/PaaS/SaaS** (EC2, Vercel, Google Docs); Regions vs AZs (≥3/region); multitenancy; IaC (Terraform)

## 🟡 Week 2 — Security & IAM 🔧
- IAM users/groups/roles/policies; root vs IAM user; authN vs authZ; MFA; least privilege
- JSON policies; roles → temp creds; AWS Budgeting; Shared Responsibility Model; SG (stateful) & NACL (stateless) intro

## 🟠 Week 3 — Compute / EC2 🔧
- AMI, instance types, key pairs, security groups; **EBS vs instance store**; **Elastic IP vs auto-assigned IP**
- Pricing (on-demand/reserved/spot) 🔧; 🚩 SSH (`ssh-keygen`, `ssh -i`, `known_hosts`, `-R`); 🚩 **cloud-init** (`#cloud-config`, `users`, `packages`, `write_files`, `runcmd`)

## 🔴 Week 4 — VPC & Networking
- 🚩 VPC (region-level; default 172.31.0.0/16 vs non-default); 🚩 CIDR (/16–/28, RFC 1918, blocked ranges, classful vs classless, VLSM, subnetting math, supernets)
- 🚩 Subnets (AZ-level, subset, public vs private); route tables (`0.0.0.0/0`, main vs custom); IGW; NAT
- 🚩 **SG (stateful) vs NACL (stateless)**; peering; VPN (AES 128/256); Direct Connect; *(skim: Route 53, CloudFront)*

## 🟠 Week 5 — AWS CLI + Bash
- v1 vs v2; install/PATH; `aws login --remote`; `~/.aws` + profiles; `aws <service> <sub> [opts]`
- 🚩 `--output`; 🚩 JMESPath `--query` (`[*]`, `[-1]`, `sort_by`, `|`); key-pair ops; `describe-images` + `--filters`; 🚩 `file://` vs `fileb://`
- 🚩 Bash: shebang, `set -euo pipefail`, `$# $1 $*`, `$( )`, heredoc `<<EOF`, `[[ ]]`, functions/`local`, `>&2`, `exit`, ANSI color

## 🟠 Week 7 — AWS Storage Services (NEW — on the midterm)
- 🚩 **S3** (object storage): 11-nines durability, 99.99% availability/SLA, 5 TB objects, storage classes, lifecycle, Object Lock (WORM), use cases (hosting, data lakes, backup, serverless)
- 🚩 **EBS** (block storage): boot volumes, volume types (gp2/gp3, io1/io2/io2 Block Express, st1, sc1), Elastic Volumes, snapshots, AES-256/KMS, Multi-Attach
- 🚩 **EFS** (file storage): NFS 4.0/4.1, shared multi-EC2 + on-prem, auto-scaling to PB, 11-nines durability, access points, lifecycle tiers
- 🚩 **FSx**: Windows File Server (SMB + AD), Lustre (HPC + S3), NetApp ONTAP (multiprotocol), OpenZFS
- 🚩 **Storage Gateway**: S3 File Gateway, FSx File Gateway, Volume Gateway (cached/stored), Tape Gateway
- 🚩 **AWS Backup**: centralized policy-based backup, KMS default, cross-region/account, immutable vaults
- 🚩 **"Elastic"** terminology; 🚩 **storage comparison / scenario selection**

## 🚩 Cross-cutting (midterm emphasis)
- 🚩 **Stateless vs stateful** — network (HTTP) + VPC (NACL vs SG)
- 🚩 **"Elastic" meaning**; 🚩 **cloud-init** (recurring); 🚩 **AWS CLI** (reused across weeks)

---

# Part 2 — Comprehensive study guide

*(Weeks 1–5 sections are unchanged and kept below in condensed-but-complete form; Week 7 is new and deep.)*

## 🟡 Week 1 — Cloud fundamentals

**NIST definition:** on-demand, ubiquitous, convenient network access to a shared pool of configurable computing resources, rapidly provisioned/released with minimal effort. **Consumption-based pricing** = pay for what you use (⚠️ models vary by service).

**Deployment models:** Public (third-party CSP, shared — AWS) · Community (similar-need orgs pool resources) · Private (dedicated to one org; ⚠️ on-prem ≠ private, private need not be on-prem) · Hybrid (public + private — AWS + your data center).

**Service models (heavily tested — you saw these on the test):**

| Model | You manage | Example |
|---|---|---|
| **IaaS** | OS and up | **EC2**, VPS |
| **PaaS** | app + data only | **Vercel** |
| **SaaS** | end user | **Google Docs** |

**Regions vs AZs:** Region = geographic area (`us-west-2`, `ca-central-1`); AZ = isolated location within a region (≥3 AZs per region); `us-west-2a/b/c`. Multitenancy = shared infra, logical isolation. IaC = provision via code (Terraform/OpenTofu).

## 🟡 Week 2 — Security & IAM 🔧

- **IAM user / group / role / policy**; **role** → temporary credentials.
- **Root user** = account owner (⚠️ never for daily work); **MFA** = 2nd factor; **least privilege** = minimum permissions.
- **Authentication** (who you are) vs **authorization** (what you can do).
- **Shared Responsibility Model:** AWS = security *of* the cloud (hardware/hypervisor); you = security *in* the cloud (IAM, data, OS patching, SGs). ⚠️ "who patches guest OS?" → you.
- **Budgeting:** set budgets + alerts to monitor spend (⚠️ alerts, not auto-stop, unless budget actions).

## 🟠 Week 3 — Compute / EC2 🔧

- **AMI** = template (OS + software); **instance type** = CPU/mem/storage/network config; **key pair** = AWS keeps public, you keep private; **SG** = instance firewall.

| Feature | EBS volume | Instance store |
|---|---|---|
| Persistence | **persistent** | **ephemeral** (lost on stop/hibernate/**terminate**) |

| Feature | Elastic IP | Auto-assigned public IP |
|---|---|---|
| Lifetime | yours until **released** | lost on stop/terminate |
| Reassignment | **can remap** | **cannot** |

**Pricing 🔧:** On-Demand (no commitment) · Reserved (1–3 yr commitment, discount) · Spot (up to ~90% off, ⚠️ **can be interrupted**).

**SSH 🚩:**
```bash
ssh-keygen -f .ssh/aws -C "aws lab key"   # generate key pair
ssh -i .ssh/aws admin@<ip-address>        # connect (admin = default Debian user)
ssh-keygen -R <host>                       # remove host from known_hosts
```

**cloud-init 🚩 (recurring — likely tested).** `#cloud-config` YAML: `users:` (create user + inject public key), `packages:` (install nginx), `write_files:` (write `/var/www/html/index.html`, owner `web:web`, `permissions: '0644'`), `runcmd:` (mkdir/chown/chmod + `systemctl enable/restart nginx`). Diagnose with `cloud-init status --long`; test with `curl http://<ip>`. ⚠️ Most failures = YAML formatting.

## 🔴 Week 4 — VPC & Networking (deep — unchanged)

- **VPC** = logically isolated virtual network, **region-level**. **Default** VPC (auto, one per region, CIDR 172.31.0.0/16, preconfigured internet, one default subnet per AZ) vs **non-default** (you configure everything).
- **CIDR 🚩:** `IP/prefix`; prefix = network bits. `/16`=65,536 · `/24`=256 (254 usable) · `/28`=16 (min VPC). **VPC CIDR must be /16–/28.** **Blocked:** `0.0.0.0/8`, `127.0.0.0/8`, `169.254.0.0/16`, `224.0.0.0/4`. **RFC 1918:** `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`.
- **Subnetting (4 moves):** prefix→mask → block size = 256−last-octet → list starts → usable = block−2. Split 172.16.0.0/16 into ≥10 subnets → 4 extra bits → **/20** (4094 hosts each).
- **Subnets:** CIDR subset of VPC, **single AZ**. **Public** = has route to IGW; **private** = no IGW route.
- **Route tables:** `0.0.0.0/0` = default route; main vs custom; subnet associations. **IGW** = attach to VPC → enables public internet. **NAT** = outbound-only internet for private subnets.
- **SG vs NACL 🚩:**

| Feature | Security Group | NACL |
|---|---|---|
| Level | instance (ENI) | subnet |
| State | **stateful** | **stateless** |
| Default | no inbound, all outbound | allow all in/out |
| Rules | allow only | allow **and deny** |
| Eval | all rules | lowest number first |
| Return traffic | **automatic** | **must be explicit (ephemeral 1024–65535)** |

- **Connectivity:** VPC peering (2 VPCs, private, same/cross-region) · VPN (over internet, virtual private gateway + customer gateway, AES 128/256, ≤10/VPC) · Direct Connect (dedicated 1/10 Gbps private line, ⚠️ no internet, low latency, pricier).

## 🟠 Week 5 — AWS CLI + Bash (unchanged)

Command structure: `aws <service> <subcommand> [options]` (e.g. `aws ec2 describe-key-pairs --output text`).

```bash
# all key names (text); default output is JSON
aws ec2 describe-key-pairs --query 'KeyPairs[*].KeyName' --output text

# newest key name (sort + last)
aws ec2 describe-key-pairs --query 'KeyPairs | sort_by(@, &CreateTime) | [-1].KeyName' --output text

# import a key (raw binary)
aws ec2 import-key-pair --key-name "bcit-demo" --public-key-material fileb://~/.ssh/aws.pub
```

- `file://` (encoded) vs **`fileb://`** (raw binary — use for SSH keys). `--output text|yaml|json`. JMESPath: `[*]`, `[0]`, `[-1]`, `sort_by(@,&field)`, `|`.
- **Bash:** `#!/usr/bin/env bash` · `set -euo pipefail` · `$#`/`$1`/`$*` · `$( )` command substitution · `cat > f <<EOF … EOF` heredoc · `[[ -f ]]`/`[[ -ne ]]` · `local` · `>&2` · `&>/dev/null` · `exit 1` · ANSI `\033[1;31m`.

**Two canonical scripts (memorize the pattern):**
1. **Import key** — validate `$# -ne 1`, check `[[ ! -f "$1" ]]`, detect duplicate via `aws ec2 describe-key-pairs --key-names "$key_name" &>/dev/null`, then `import-key-pair --public-key-material fileb://… > key_data`.
2. **Get latest Debian AMI** — `ami_id=$(aws ec2 describe-images --owners 136693071363 --filters … --query 'sort_by(Images, &CreationDate)[-1].ImageId' --output text)` then `cat > ami.txt <<EOF` writing `debian_ami=${ami_id}`.

## 🟠 Week 7 — AWS Storage Services (NEW — deep)

**Six services, three storage paradigms + hybrid + backup.** Memorize **what each is (object/block/file)** and **when to use it** — that's the scenario-question axis.

### Storage categories at a glance

| Paradigm | Service | Key trait |
|---|---|---|
| **Object** | **S3** | flat objects, HTTP(S) access, unlimited, 11-nines durability |
| **Block** | **EBS** | raw volumes for EC2 (boot/DB), low latency, single-instance |
| **File** | **EFS** (NFS) / **FSx** (SMB/Lustre/…) | shared file system, multiple servers at once |
| **Hybrid bridge** | **Storage Gateway** | connect on-prem ↔ AWS |
| **Data protection** | **AWS Backup** | centralized policy-based backup |

### Amazon S3 — object storage

- **Object storage**, unlimited scalability, no capacity provisioning. Objects up to **5 TB**. Accessed via console, CLI, SDKs, REST.
- **Durability 99.999999999% ("11 nines")** = data automatically distributed across **multiple AZs**; **availability 99.99%** (SLA-backed). ⚠️ Not every class is multi-AZ — **One Zone-IA & Express One Zone are single-AZ** (lower redundancy).
- **Security:** SSL/TLS in transit; SSE/KMS or client-side at rest; IAM roles, bucket policies; **Object Lock** = WORM (write-once-read-many) for compliance.
- **Use cases:** static website assets/app backends; **data lakes** (Athena, Redshift, EMR); backup/DR (**lifecycle policies** move to cheaper tiers or delete); serverless (Lambda/SNS/SQS triggers on upload).

**S3 storage classes (scenario goldmine):**

| Class | Access pattern | Notes |
|---|---|---|
| **S3 Standard** | frequent, default | ≥3 AZs, low latency/high throughput |
| **Intelligent-Tiering** | unpredictable | auto-moves between 5 tiers (Frequent→Deep Archive); same durability/latency |
| **Express One Zone** | speed-critical, single-AZ OK | sub-ms latency; Local Zones/Outposts; **no cross-AZ** |
| **Standard-IA** | infrequent but instant when needed | 11-nines durability, 99.9% availability, **retrieval fees**, cheaper storage |
| **One Zone-IA** | infrequent, single-AZ OK | 99.5% availability, no cross-AZ |
| **Glacier Instant Retrieval** | archive, on-demand | millisecond retrieval |
| **Glacier Flexible Retrieval** | archive, occasional | minutes (expedited) to hours (bulk) |
| **Glacier Deep Archive** | rarely/never | **12–48 hr retrieval**, cheapest |

Extra S3: **Transfer Acceleration** (CloudFront edge locations speed cross-region uploads); **S3 on Outposts / Directory buckets** (data residency).

### Amazon EBS — block storage (boot + database)

- **Block storage**, the **main boot storage for EC2**. Replicates **within its AZ** (⚠️ single-AZ scope — snapshots are how you go cross-AZ/region). AFR 0.1–0.2%. Consistent low latency.
- **Elastic Volumes** = resize volume size/performance/type **without stopping the instance**.
- **Volume types:**

| Type | Use | Notes |
|---|---|---|
| **gp2 / gp3** (General SSD) | boot, dev, general | gp3 baseline **3,000 IOPS / 125 MiB/s**, up to 80k IOPS |
| **io1 / io2 / io2 Block Express** (Provisioned IOPS SSD) | mission-critical DB | up to 256k IOPS, sub-ms, 64 TB; **io2 Block Express = Multi-Attach** |
| **st1** (Throughput HDD) | big data / warehouse | throughput (MB/s) > IOPS |
| **sc1** (Cold HDD) | infrequent, cheap | lowest-cost HDD |

- **Snapshots** = point-in-time, **incremental** (only changed blocks) → new volumes, cross-AZ/region, account sharing, Data Lifecycle Manager.
- **Multi-Attach (io2 Block Express):** one volume → multiple EC2 instances **same AZ** (app must coordinate writes). ⚠️ Not for all volume types.
- Encryption **AES-256 via KMS**, at rest + in transit.

### Amazon EFS — file storage (shared NFS)

- **File storage** over **NFS 4.0/4.1**. **Multiple EC2 (and on-prem Linux) read/write the SAME file system simultaneously** → shared file workloads.
- **Auto-scales** up to petabytes (grows/shrinks on demand — this is why it's "Elastic"). Regional (multi-AZ), **11-nines durability, 99.99% availability**.
- **Lifecycle** tiers (IA/Archive) move old files automatically; **access points** give per-app root + POSIX permissions.
- ⚠️ Use EFS when you need a **shared file system** for many Linux servers (not object, not single-instance block).

### Amazon FSx — managed high-performance file systems

| Variant | Protocol | Use |
|---|---|---|
| **FSx for Windows File Server** | **SMB** + Active Directory | Windows enterprise shares, quotas, backups |
| **FSx for Lustre** | POSIX (Linux) | **HPC / big data**, integrates with S3 |
| **FSx for NetApp ONTAP** | NFS + SMB + iSCSI | multiprotocol, dedup, SnapMirror DR |
| **FSx for OpenZFS** | ZFS | Linux, snapshots/clones, data integrity |

⚠️ **EFS vs FSx:** EFS = general shared **NFS** (Linux), auto-scaling; FSx = specialized — **Windows/SMB** (Windows File Server) or **HPC** (Lustre).

### AWS Storage Gateway — hybrid on-prem ↔ AWS

Deployed as a **VM (VMware / Hyper-V / KVM) or EC2 instance**; caches hot data locally for low latency.

| Gateway | Protocol | Backed by |
|---|---|---|
| **S3 File Gateway** | NFS / SMB | presents S3 as a file share |
| **FSx File Gateway** | SMB | exposes FSx (Windows File Server) |
| **Volume Gateway** | iSCSI (block) | cached mode (data in S3) or stored mode (data on-prem, backups→S3) |
| **Tape Gateway** | virtual tape library (VTL) | replaces physical tape; tapes → S3/Glacier |

### AWS Backup — centralized data protection

- **Centralized, policy-based backup** across AWS + hybrid (Storage Gateway, VMware) from one console/CLI/API.
- Backup **plans** (what/how often/how long), schedules, retention, lifecycle → cold storage, **KMS-encrypted by default**.
- Cross-region/account copies for DR; RTO/RPO; **vaults are immutable** (write-once).

### 🚩 What does "Elastic" mean? (professor's example)

**"Elastic" = the resource can automatically scale up/down on demand and be dynamically provisioned/released without manual effort or downtime.**

| Service | Why "Elastic" |
|---|---|
| **Elastic IP** | static public IPv4 you can allocate, **remap** to another instance, and release on demand |
| **Elastic Block Store (EBS)** | volumes **resize dynamically** (Elastic Volumes) without stopping the instance |
| **Elastic File System (EFS)** | **auto-scales** to petabytes as demand changes |
| **Elastic Load Balancing** | scales load balancing with traffic |

⚠️ **Trap:** "Elastic" means **dynamic/scalable**, *not* "free."

### 🚩 Storage scenario cheatsheet ("pick the most appropriate service")

| Scenario | Answer |
|---|---|
| Static website, images, media, backups, data lake | **S3** |
| Boot/OS disk for one EC2; low-latency DB on one instance | **EBS** (gp3; io2 for DB) |
| High-throughput big data / warehouse (single instance) | **EBS st1** |
| Shared file system, many Linux EC2 at once | **EFS** (NFS) |
| Windows file shares + Active Directory | **FSx for Windows File Server** |
| HPC / ML with massive throughput + S3 data | **FSx for Lustre** |
| On-prem apps need S3 as a file share | **Storage Gateway — S3 File Gateway** |
| Replace physical tape backups | **Storage Gateway — Tape Gateway** |
| Centralized backups across many AWS services | **AWS Backup** |
| Rarely-accessed archive, cheapest, can wait hours | **S3 Glacier Deep Archive** |
| Infrequent access but instant retrieval | **S3 Standard-IA** / **Glacier Instant Retrieval** |
| Compliance WORM (immutable) | **S3 Object Lock** / **AWS Backup vault lock** |

## 🚩 Cross-cutting (unchanged): Stateless vs Stateful

- **Network (HTTP):** stateless = each request independent; server remembers nothing. Web apps fake state with client-side **cookies/tokens**. (⚠️ don't confuse with TCP being connection-oriented at transport layer.)
- **VPC:** **SG = stateful** (return traffic auto-allowed, no ephemeral rule); **NACL = stateless** (must explicitly allow return + **ephemeral ports 1024–65535**).

---

# Part 3 — MIDTERM practice test (mirrors the real format, "hard")

## Section A — 20 "select all that apply" (A–F)

**A1.** Which are TRUE about **EC2**? (Select all that apply.)
A. An AMI is a preconfigured template containing the OS and software.
B. Instance store data persists after a terminate.
C. AWS stores the public key; you store the private key.
D. A security group specifies protocols/ports that can reach the instance.
E. EBS is the main boot storage for EC2.
F. An Elastic IP can be remapped to another instance.

**A2.** Which are TRUE about **EC2 pricing models**? (Select all that apply.)
A. On-Demand has no upfront commitment.
B. Spot instances can be interrupted by AWS.
C. Reserved Instances require a commitment (typically 1–3 years) for a discount.
D. Spot is the best choice for a stateful, non-interruptible database.
E. On-Demand gives the largest discount.
F. Reserved Instances give no discount.

**A3.** Which **service-model pairings** are correct? (Select all that apply.)
A. EC2 — IaaS
B. Vercel — PaaS
C. Google Docs — SaaS
D. EC2 — PaaS
E. Google Docs — IaaS
F. Vercel — IaaS

**A4.** Which are TRUE about **IAM**? (Select all that apply.)
A. A role provides temporary credentials.
B. The root user should be used for daily tasks.
C. A policy is a JSON document defining permissions.
D. A group is a collection of IAM users.
E. Least privilege means granting maximum permissions.
F. MFA provides a second factor of authentication.

**A5.** Which are **valid CIDR blocks for a VPC**? (Select all that apply.)
A. 10.0.0.0/16
B. 10.0.0.0/8
C. 10.0.0.0/28
D. 10.0.0.0/29
E. 172.31.0.0/16
F. 192.168.0.0/24

**A6.** Which are TRUE about **subnets**? (Select all that apply.)
A. A subnet's CIDR must be a subset of its VPC's CIDR.
B. A subnet spans multiple Availability Zones.
C. A subnet lives in exactly one Availability Zone.
D. A subnet with a route to an internet gateway is public.
E. A VPC must contain at least two subnets.
F. A subnet can have a /29 CIDR if the VPC is /16.

**A7.** Which are TRUE about **security groups vs NACLs** (statefulness)? (Select all that apply.)
A. A security group is stateful.
B. A NACL is stateless.
C. A security group requires an explicit rule for return traffic.
D. A NACL requires explicit rules for return traffic (ephemeral ports).
E. A security group automatically allows reply traffic.
F. A NACL automatically allows reply traffic.

**A8.** What does **"Elastic"** mean in AWS services? (Select all that apply.)
A. Resources can scale up/down on demand automatically.
B. Resources are permanently fixed in size.
C. It implies dynamic provisioning/release without manual effort.
D. An Elastic IP is a static public IP you can remap or release.
E. EBS volumes can be resized without downtime.
F. "Elastic" always means "free of charge."

**A9.** Which are TRUE about the **AWS CLI**? (Select all that apply.)
A. `aws` is the top-level command for both v1 and v2.
B. The default output of `describe-key-pairs` is JSON.
C. `fileb://` reads a file as raw binary.
D. `--query` uses JMESPath expressions.
E. `aws login` should be run as the root user.
F. Configuration is stored in ~/.aws in INI format.

**A10.** In `set -euo pipefail`, which are TRUE? (Select all that apply.)
A. `-e` exits the script on any command error.
B. `-u` errors on unset variables.
C. `-o pipefail` makes a pipeline fail if any command in it fails.
D. `-e` ignores errors.
E. `-u` makes variables global.
F. `$#` gives the number of positional arguments.

**A11.** Which are TRUE about **cloud-init**? (Select all that apply.)
A. `#cloud-config` signals YAML configuration.
B. `packages:` installs software such as nginx.
C. `write_files:` writes files with owner/permissions.
D. `runcmd:` commands run before networking is up.
E. It is the industry-standard multi-distribution instance-init tool.
F. `cloud-init status --long` helps diagnose failures.

**A12.** Which are TRUE about **Amazon S3**? (Select all that apply.)
A. It offers 11-nines (99.999999999%) durability.
B. S3 Standard replicates data across at least three AZs.
C. A single object can be up to 5 TB.
D. S3 One Zone-IA stores data across multiple AZs.
E. It is object storage with effectively unlimited scalability.
F. You must provision storage capacity in advance.

**A13.** Which are TRUE about **S3 storage classes**? (Select all that apply.)
A. S3 Standard is the default, for frequently accessed data.
B. S3 Standard-IA is for infrequent access and charges retrieval fees.
C. S3 Glacier Deep Archive retrieval takes 12–48 hours and is cheapest.
D. S3 Intelligent-Tiering automatically moves data between tiers.
E. S3 Express One Zone is multi-AZ.
F. S3 Glacier Instant Retrieval offers millisecond retrieval.

**A14.** Which are TRUE about **EBS**? (Select all that apply.)
A. EBS is block storage.
B. gp3 provides a baseline of 3,000 IOPS.
C. io2 Block Express supports Multi-Attach.
D. EBS replicates data within its Availability Zone.
E. EBS snapshots are full (non-incremental) copies.
F. EBS volumes can be encrypted with AES-256 via KMS.

**A15.** Which are TRUE about **EFS vs FSx**? (Select all that apply.)
A. EFS uses the NFS protocol.
B. EFS can be shared by multiple EC2 instances simultaneously.
C. FSx for Windows File Server uses SMB and integrates with Active Directory.
D. FSx for Lustre is designed for HPC/big data workloads.
E. EFS is object storage.
F. EFS scales automatically to petabytes.

**A16.** Which are TRUE about **Storage Gateway**? (Select all that apply.)
A. S3 File Gateway presents S3 as an NFS/SMB file share.
B. Volume Gateway uses iSCSI.
C. Tape Gateway replaces physical tape with a virtual tape library.
D. Storage Gateway can run as a VMware/Hyper-V/KVM VM or an EC2 instance.
E. Storage Gateway supports only block storage.
F. Tape Gateway stores virtual tapes in S3/Glacier.

**A17.** Which are TRUE about **AWS Backup**? (Select all that apply.)
A. It centralizes policy-based backup management.
B. Backup vaults are immutable.
C. Backups are encrypted with KMS by default.
D. Backups can be copied across regions and accounts.
E. Backups are unencrypted by default.
F. It integrates with Storage Gateway and VMware.

**A18.** A company needs a **shared file system that many Linux EC2 instances read/write simultaneously**, and it must **scale automatically**. Which service is most appropriate? (Select all that apply.)
A. Amazon S3
B. Amazon EBS
C. Amazon EFS
D. Amazon FSx for Lustre
E. AWS Storage Gateway — Volume Gateway
F. AWS Backup

**A19.** Which are TRUE about **Elastic IP vs auto-assigned public IP**? (Select all that apply.)
A. An Elastic IP is a static public IPv4.
B. An auto-assigned public IP is lost when the instance stops.
C. An Elastic IP cannot be remapped.
D. An Elastic IP persists until you release it.
E. An auto-assigned public IP can be reassigned to a different instance.
F. An Elastic IP is a private IPv4 address.

**A20.** Which are TRUE about **regions, AZs, and durability**? (Select all that apply.)
A. A Region contains multiple Availability Zones.
B. Each AWS Region has at least three AZs.
C. A VPC spans a single Availability Zone.
D. A subnet lives in a single Availability Zone.
E. S3 Standard achieves 11-nines durability by distributing across AZs.
F. An Availability Zone spans multiple Regions.

## Section B — 10 short-answer

**B1.** What does "Elastic" mean in AWS services? Name two AWS services and explain why each is "elastic."

**B2.** Name the three storage paradigms (object / block / file) and give one AWS service for each.

**B3.** Which S3 storage class is for rarely-accessed data with 12–48 hour retrieval, and why would you choose it?

**B4.** What are the baseline IOPS and throughput of an EBS gp3 volume, and what does "Elastic Volumes" let you do?

**B5.** Which EBS volume type supports attaching one volume to multiple EC2 instances (Multi-Attach), and in what scope (AZ/region)?

**B6.** What protocol does EFS use, and how many EC2 instances can read/write the same file system at once?

**B7.** FSx for Windows File Server uses which protocol and integrates with what Microsoft service?

**B8.** Which Storage Gateway replaces physical tape backups, and where are the "tapes" actually stored?

**B9.** Explain the difference between S3's 11-nines **durability** and 99.99% **availability**.

**B10.** Which storage service would you use for the **boot volume** of a single EC2 instance, and why not EFS or S3?

## Section C — Written response

**C1 (VPC design).** Given VPC `10.0.0.0/16` in `us-west-2`, design a two-tier setup (public web + private database).
- (a) Choose subnets (AZs + CIDRs) and justify why your CIDRs are valid.
- (b) List the resources and exact routes/associations that make one subnet public and the other private.
- (c) How does the database get software updates without being internet-reachable? Name the resource.
- (d) What should a SG vs a NACL each allow for SSH, and why does one need extra return-traffic rules?

**C2 (Bash).** Write a complete Bash script that takes a key name + public key path, validates the file, checks if the key already exists in AWS, imports it with `fileb://`, and prints a red error + exits 1 on failure. Show the run command and sample success/failure output.

**C3 (Stateless — network).** Explain what it means for HTTP to be stateless, contrast with a stateful interaction, and explain how web apps simulate state.

**C4 (Stateless — VPC).** SSH works via a security group (inbound TCP 22). Replacing the SG with a NACL that allows TCP 22 inbound breaks SSH. Explain precisely why using *stateful*, *stateless*, and *ephemeral ports*, and state the missing rule.

**C5 (Storage scenario).** For EACH scenario, name the single most appropriate AWS service and justify in one sentence:
- (a) Store 5 PB of rarely-accessed legal records that must be kept 7 years for compliance (cheapest, retrieval can wait a day).
- (b) A Windows-based department needs a shared file server with Active Directory permissions.
- (c) An on-premises data center wants to keep using its existing file-server interface while tiering old files to the cloud.
- (d) Run a high-throughput machine-learning job that reads data already sitting in S3.
- (e) Provide the OS boot disk for a single EC2 web server.

---

## Answer key

### Section A

**A1 → A, D, E, F.** B ✘ (instance store is lost on terminate). C ✘ (AWS keeps **public**, you keep **private**).

**A2 → A, B, C.** D ✘ (Spot is interruptible — bad for stateful non-interruptible DB). E ✘ (Reserved gives the bigger discount). F ✘ (Reserved *does* discount).

**A3 → A, B, C.** D ✘ (EC2 is IaaS). E ✘ (Google Docs is SaaS). F ✘ (Vercel is PaaS).

**A4 → A, C, D, F.** B ✘ (never use root daily). E ✘ (least privilege = minimum).

**A5 → A, C, E, F.** B ✘ (/8 exceeds the /16 max). D ✘ (/29 is below the /28 minimum).

**A6 → A, C, D.** B ✘ (subnet is single-AZ). E ✘ (needs ≥1). F ✘ (subnet CIDR must also be /16–/28).

**A7 → A, B, D, E.** C ✘ (SG needs **no** return rule — stateful). F ✘ (NACL does **not** auto-allow return).

**A8 → A, C, D, E.** B ✘ ("Elastic" = dynamic, opposite of fixed). F ✘ ("Elastic" ≠ free).

**A9 → A, B, C, D, F.** E ✘ (never root).

**A10 → A, B, C, F.** D ✘. E ✘ (`-u` doesn't make vars global).

**A11 → A, B, C, E, F.** D ✘ (`runcmd` runs near the **end** of boot).

**A12 → A, B, C, E.** D ✘ (One Zone-IA = **single** AZ). F ✘ (S3 needs no capacity provisioning).

**A13 → A, B, C, D, F.** E ✘ (Express One Zone = single-AZ).

**A14 → A, B, C, D, F.** E ✘ (snapshots are **incremental**).

**A15 → A, B, C, D, F.** E ✘ (EFS is **file** storage, not object).

**A16 → A, B, C, D, F.** E ✘ (Storage Gateway supports file AND block AND tape).

**A17 → A, B, C, D, F.** E ✘ (KMS-encrypted **by default**).

**A18 → C only.** EFS = general shared NFS, auto-scaling. A ✘ (S3 is object, not a live shared file system). B ✘ (EBS is single-instance block; Multi-Attach is niche io2 only). D ✘ (FSx for Lustre is **HPC-specific**, not general shared NFS). E ✘ (Volume Gateway is iSCSI block, on-prem hybrid). F ✘ (Backup is protection, not live storage).

**A19 → A, B, D.** C ✘ (EIP *can* be remapped). E ✘ (auto-assigned IP **cannot** be reassigned). F ✘ (EIP is **public**).

**A20 → A, B, D, E.** C ✘ (VPC spans the whole **region**). F ✘ (an AZ is within a region).

### Section B

**B1.** "Elastic" = resources **scale up/down on demand** and are **dynamically provisioned/released** without manual effort or downtime. Examples: **Elastic IP** (static public IP you remap/release on demand), **Elastic Block Store** (volumes resize dynamically via Elastic Volumes without stopping the instance), **Elastic File System** (auto-scales to petabytes).

**B2.** Object → **S3**; Block → **EBS**; File → **EFS** (or FSx).

**B3.** **S3 Glacier Deep Archive** — cheapest storage for rarely/never-accessed data; you accept 12–48 hr retrieval.

**B4.** **3,000 IOPS** baseline, **125 MiB/s** throughput. **Elastic Volumes** let you change size/performance/type **without stopping the instance**.

**B5.** **io2 Block Express** (Provisioned IOPS SSD), and only across instances **in the same Availability Zone**.

**B6.** **NFS 4.0/4.1**; **multiple** EC2 instances (and on-prem Linux servers) simultaneously.

**B7.** **SMB** protocol; integrates with **Active Directory**.

**B8.** **Tape Gateway**; virtual tapes are stored in **S3** (archivable to **Glacier**).

**B9.** **Durability (11 nines = 99.999999999%)** = probability your *data is not lost* over a year (copies across AZs). **Availability (99.99%)** = percentage of time the service is *reachable/operational* (SLA-backed). A file can be perfectly durable but momentarily unavailable.

**B10.** **EBS** — block storage designed as the boot volume for an EC2 instance. **EFS** is a shared file system (wrong granularity/overhead for a single boot disk); **S3** is object storage (can't be a root filesystem).

### Section C

**C1.** (a) Public `10.0.1.0/24` in `us-west-2a`; private `10.0.2.0/24` in `us-west-2b` — both valid (/24 within /16–/28, subsets of 10.0.0.0/16). (b) Create IGW → attach to VPC → add `0.0.0.0/0 → IGW` to the **public** subnet's route table (or main table); associate the **private** subnet with a route table that has **no** IGW route; enable auto-assign public IP on the public subnet. (c) A **NAT gateway** in the public subnet; the private subnet's route table gets `0.0.0.0/0 → NAT` for outbound-only internet. (d) SG: inbound TCP 22 from your IP only (stateful — reply auto-allowed). NACL: inbound TCP 22 **plus** outbound ephemeral ports 1024–65535 (stateless — explicit return path required).

**C2.** (see Week 5 import script pattern, parameterized for key name.) Run `./import.sh mykey ~/.ssh/aws.pub`; success `Imported 'mykey'.`; failure `ERROR: File does not exist: /bad/path` (red, exit 1).

**C3.** HTTP is **stateless**: each request is self-contained and independent; the server keeps **no memory** between requests. A **stateful** interaction remembers context (a logged-in session, a tracked connection). Web apps simulate state with **client-side cookies/tokens** resent on each request, so the server stays stateless.

**C4.** The **security group is stateful** — it tracks the connection, so once inbound 22 is allowed the **reply is auto-permitted**. A **NACL is stateless** — it tracks no connection, so inbound 22 alone is insufficient: the **outbound** reply to the client's **ephemeral port (1024–65535)** is dropped. Fix: add an outbound NACL rule allowing TCP 1024–65535 to the client (and ensure the inbound rule is evaluated first by rule number).

**C5.** (a) **S3 Glacier Deep Archive** — cheapest, retrieval latency acceptable for 7-yr compliance. (b) **FSx for Windows File Server** — SMB + Active Directory. (c) **Storage Gateway (S3 File Gateway)** — presents S3 as a file share, keeps on-prem interface, tiers to S3. (d) **FSx for Lustre** — HPC throughput, natively reads S3 data. (e) **EBS** — block storage is the EC2 boot volume.

---

*End of midterm guide. Priority: memorise the storage paradigm→service mapping and the SG-vs-NACL stateless rule, re-run your past lab scripts, and re-take past quiz questions closed-book.*
