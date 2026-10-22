# 3640 Midterm Practice — 3 Full Versions (Hard)

> **Scope:** Weeks 1–7. **Format (matches the real test):** 20 "select all that apply" (A–F) · 10 short-answer · written response (VPC, bash, 2 stateless, storage).
> **How to use:** attempt each version **closed-book** on a blank page, then grade with the key. Each version has **different questions/scenarios**, so they're genuinely re-testable. Time yourself ~50 min/version.

---

# VERSION 1

## Section A — 20 select-all-that-apply (A–F)

**1.** Which are TRUE about **EC2**?
A. An AMI is a preconfigured template containing the OS and software.
B. Instance store data persists after a terminate.
C. AWS stores the public key; you store the private key.
D. A security group filters protocols/ports/source IPs to an instance.
E. EBS is the main boot storage for EC2.
F. An Elastic IP can be remapped to another instance.

**2.** Which are TRUE about **EC2 pricing**?
A. On-Demand has no upfront commitment.
B. Spot instances can be interrupted by AWS.
C. Reserved Instances require a commitment for a discount.
D. Spot is best for a stateful, non-interruptible database.
E. On-Demand gives the largest discount.
F. Reserved Instances give no discount.

**3.** Which **service-model pairings** are correct?
A. EC2 — IaaS
B. Vercel — PaaS
C. Google Docs — SaaS
D. EC2 — PaaS
E. Google Docs — IaaS
F. Vercel — IaaS

**4.** Which are TRUE about **IAM**?
A. A role provides temporary credentials.
B. The root user should be used for daily tasks.
C. A policy is a JSON document defining permissions.
D. A group is a collection of IAM users.
E. Least privilege means granting maximum permissions.
F. MFA provides a second factor of authentication.

**5.** Which are **valid CIDR blocks for a VPC**?
A. 10.0.0.0/16
B. 10.0.0.0/8
C. 10.0.0.0/28
D. 10.0.0.0/29
E. 172.31.0.0/16
F. 192.168.0.0/24

**6.** Which are TRUE about **subnets**?
A. A subnet's CIDR must be a subset of its VPC's CIDR.
B. A subnet spans multiple Availability Zones.
C. A subnet lives in exactly one Availability Zone.
D. A subnet with a route to an internet gateway is public.
E. A VPC must contain at least two subnets.
F. A subnet can have a /29 CIDR if the VPC is /16.

**7.** Which are TRUE about **security groups vs NACLs** (statefulness)?
A. A security group is stateful.
B. A NACL is stateless.
C. A security group requires an explicit rule for return traffic.
D. A NACL requires explicit rules for return traffic (ephemeral ports).
E. A security group automatically allows reply traffic.
F. A NACL automatically allows reply traffic.

**8.** What does **"Elastic"** mean in AWS services?
A. Resources can scale up/down on demand automatically.
B. Resources are permanently fixed in size.
C. It implies dynamic provisioning/release without manual effort.
D. An Elastic IP is a static public IP you can remap or release.
E. EBS volumes can be resized without downtime.
F. "Elastic" always means "free of charge."

**9.** Which are TRUE about the **AWS CLI**?
A. `aws` is the top-level command for both v1 and v2.
B. The default output of `describe-key-pairs` is JSON.
C. `fileb://` reads a file as raw binary.
D. `--query` uses JMESPath expressions.
E. `aws login` should be run as the root user.
F. Configuration is stored in ~/.aws in INI format.

**10.** In `set -euo pipefail`, which are TRUE?
A. `-e` exits the script on any command error.
B. `-u` errors on unset variables.
C. `-o pipefail` makes a pipeline fail if any command in it fails.
D. `-e` ignores errors.
E. `-u` makes variables global.
F. `$#` gives the number of positional arguments.

**11.** Which are TRUE about **cloud-init**?
A. `#cloud-config` signals YAML configuration.
B. `packages:` installs software such as nginx.
C. `write_files:` writes files with owner/permissions.
D. `runcmd:` commands run before networking is up.
E. It is the industry-standard multi-distribution instance-init tool.
F. `cloud-init status --long` helps diagnose failures.

**12.** Which are TRUE about **Amazon S3**?
A. It offers 11-nines (99.999999999%) durability.
B. S3 Standard replicates data across at least three AZs.
C. A single object can be up to 5 TB.
D. S3 One Zone-IA stores data across multiple AZs.
E. It is object storage with effectively unlimited scalability.
F. You must provision storage capacity in advance.

**13.** Which are TRUE about **S3 storage classes**?
A. S3 Standard is the default, for frequently accessed data.
B. S3 Standard-IA is for infrequent access and charges retrieval fees.
C. S3 Glacier Deep Archive retrieval takes 12–48 hours and is cheapest.
D. S3 Intelligent-Tiering automatically moves data between tiers.
E. S3 Express One Zone is multi-AZ.
F. S3 Glacier Instant Retrieval offers millisecond retrieval.

**14.** Which are TRUE about **EBS**?
A. EBS is block storage.
B. gp3 provides a baseline of 3,000 IOPS.
C. io2 Block Express supports Multi-Attach.
D. EBS replicates data within its Availability Zone.
E. EBS snapshots are full (non-incremental) copies.
F. EBS volumes can be encrypted with AES-256 via KMS.

**15.** Which are TRUE about **EFS vs FSx**?
A. EFS uses the NFS protocol.
B. EFS can be shared by multiple EC2 instances simultaneously.
C. FSx for Windows File Server uses SMB and integrates with Active Directory.
D. FSx for Lustre is designed for HPC/big data workloads.
E. EFS is object storage.
F. EFS scales automatically to petabytes.

**16.** Which are TRUE about **Storage Gateway**?
A. S3 File Gateway presents S3 as an NFS/SMB file share.
B. Volume Gateway uses iSCSI.
C. Tape Gateway replaces physical tape with a virtual tape library.
D. Storage Gateway can run as a VMware/Hyper-V/KVM VM or an EC2 instance.
E. Storage Gateway supports only block storage.
F. Tape Gateway stores virtual tapes in S3/Glacier.

**17.** Which are TRUE about **AWS Backup**?
A. It centralizes policy-based backup management.
B. Backup vaults are immutable.
C. Backups are encrypted with KMS by default.
D. Backups can be copied across regions and accounts.
E. Backups are unencrypted by default.
F. It integrates with Storage Gateway and VMware.

**18.** A company needs a **shared file system that many Linux EC2 instances read/write simultaneously**, and it must **scale automatically**. Which service is most appropriate?
A. Amazon S3
B. Amazon EBS
C. Amazon EFS
D. Amazon FSx for Lustre
E. AWS Storage Gateway — Volume Gateway
F. AWS Backup

**19.** Which are TRUE about **Elastic IP vs auto-assigned public IP**?
A. An Elastic IP is a static public IPv4.
B. An auto-assigned public IP is lost when the instance stops.
C. An Elastic IP cannot be remapped.
D. An Elastic IP persists until you release it.
E. An auto-assigned public IP can be reassigned to a different instance.
F. An Elastic IP is a private IPv4 address.

**20.** Which are TRUE about **regions, AZs, and durability**?
A. A Region contains multiple Availability Zones.
B. Each AWS Region has at least three AZs.
C. A VPC spans a single Availability Zone.
D. A subnet lives in a single Availability Zone.
E. S3 Standard achieves 11-nines durability by distributing across AZs.
F. An Availability Zone spans multiple Regions.

## Section B — 10 short-answer

1. What does "Elastic" mean in AWS services? Name two services and why each is elastic.
2. Name the three storage paradigms (object/block/file) and one AWS service for each.
3. Which S3 class is for rarely-accessed data with 12–48 hr retrieval, and why choose it?
4. What are the baseline IOPS and throughput of EBS gp3, and what does "Elastic Volumes" let you do?
5. Which EBS volume type supports Multi-Attach, and in what scope (AZ/region)?
6. What protocol does EFS use, and how many EC2 instances can read/write the same file system at once?
7. FSx for Windows File Server uses which protocol and integrates with what Microsoft service?
8. Which Storage Gateway replaces physical tape, and where are the "tapes" stored?
9. Explain the difference between S3's 11-nines durability and 99.99% availability.
10. Which storage service for a single EC2 boot volume, and why not EFS or S3?

## Section C — Written response

**C1 (VPC).** Given VPC `10.0.0.0/16` in `us-west-2`, design a two-tier setup (public web + private DB).
(a) Choose subnets (AZs + CIDRs) and justify validity.
(b) List resources and exact routes/associations making one subnet public, the other private.
(c) How does the DB get software updates without being internet-reachable? Name the resource.
(d) What should a SG vs a NACL each allow for SSH, and why does one need extra return rules?

**C2 (Bash).** Write a Bash script that takes a key name + public key path, validates the file, checks if the key already exists in AWS, imports it with `fileb://`, and prints a red error + exits 1 on failure. Show run command + sample success/failure output.

**C3 (Stateless — network).** Explain what it means for HTTP to be stateless, contrast with stateful, and explain how web apps simulate state.

**C4 (Stateless — VPC).** SSH works via a security group (inbound TCP 22). Replacing the SG with a NACL allowing TCP 22 inbound breaks SSH. Explain using *stateful*, *stateless*, *ephemeral ports*, and state the missing rule.

**C5 (Storage scenario).** Name the most appropriate service for each and justify in one sentence:
(a) 5 PB of rarely-accessed legal records kept 7 years (cheapest, retrieval can wait a day).
(b) A Windows department needs a shared file server with AD permissions.
(c) An on-prem data center wants to keep its existing file-server interface while tiering old files to the cloud.
(d) A high-throughput ML job reading data already in S3.
(e) The OS boot disk for a single EC2 web server.

---

## VERSION 1 — Answer key

### Section A
1. **A, D, E, F.** B ✘ (instance store is lost on terminate). C ✘ (AWS keeps public, you keep private).
2. **A, B, C.** D ✘ (Spot is interruptible). E ✘ (Reserved discounts more). F ✘ (Reserved does discount).
3. **A, B, C.** D ✘ (EC2 is IaaS). E ✘ (Docs is SaaS). F ✘ (Vercel is PaaS).
4. **A, C, D, F.** B ✘ (never root daily). E ✘ (least privilege = minimum).
5. **A, C, E, F.** B ✘ (/8 exceeds /16 max). D ✘ (/29 below /28 min).
6. **A, C, D.** B ✘ (single-AZ). E ✘ (≥1, not ≥2). F ✘ (subnet also /16–/28).
7. **A, B, D, E.** C ✘ (SG needs no return rule). F ✘ (NACL doesn't auto-return).
8. **A, C, D, E.** B ✘ (opposite of elastic). F ✘ (elastic ≠ free).
9. **A, B, C, D, F.** E ✘ (never root).
10. **A, B, C, F.** D ✘. E ✘ (`-u` doesn't make vars global).
11. **A, B, C, E, F.** D ✘ (runcmd near end of boot).
12. **A, B, C, E.** D ✘ (One Zone-IA = single AZ). F ✘ (no provisioning needed).
13. **A, B, C, D, F.** E ✘ (Express One Zone = single-AZ).
14. **A, B, C, D, F.** E ✘ (snapshots incremental).
15. **A, B, C, D, F.** E ✘ (EFS is file, not object).
16. **A, B, C, D, F.** E ✘ (supports file + block + tape).
17. **A, B, C, D, F.** E ✘ (KMS by default).
18. **C.** EFS = shared NFS + auto-scale. A ✘ (object, not live shared FS). B ✘ (single-instance block). D ✘ (Lustre is HPC-specific). E ✘ (iSCSI block hybrid). F ✘ (protection, not live storage).
19. **A, B, D.** C ✘ (EIP can remap). E ✘ (auto-assigned can't reassign). F ✘ (EIP is public).
20. **A, B, D, E.** C ✘ (VPC spans region). F ✘ (AZ is within region).

### Section B
1. Elastic = scales up/down on demand + dynamically provisioned/released, no manual effort/downtime. E.g. **Elastic IP** (static public IP remapped/released on demand), **Elastic Block Store** (Elastic Volumes resize without stopping), **Elastic File System** (auto-scales to PB).
2. Object → **S3**; Block → **EBS**; File → **EFS** (or FSx).
3. **S3 Glacier Deep Archive** — cheapest; accept 12–48 hr retrieval.
4. **3,000 IOPS** baseline, **125 MiB/s**; Elastic Volumes resize size/perf/type **without stopping the instance**.
5. **io2 Block Express**; only instances **in the same AZ**.
6. **NFS 4.0/4.1**; **multiple** EC2 (and on-prem Linux) at once.
7. **SMB**; **Active Directory**.
8. **Tape Gateway**; virtual tapes stored in **S3** (archivable to **Glacier**).
9. Durability (11 nines) = probability data is **not lost** over a year (AZ copies). Availability (99.99%) = % of time service is **reachable** (SLA). Data can be durable but momentarily unavailable.
10. **EBS** (block boot volume). EFS = shared file (wrong granularity/overhead); S3 = object (can't be root FS).

### Section C
- **C1.** (a) Public `10.0.1.0/24` in `us-west-2a`, private `10.0.2.0/24` in `us-west-2b` (both valid /24 subsets). (b) IGW → attach VPC → `0.0.0.0/0 → IGW` on the public subnet's route table; private subnet associated with a table with no IGW route; enable auto-assign public IP on public subnet. (c) **NAT gateway** in public subnet; private route `0.0.0.0/0 → NAT`. (d) SG: inbound TCP 22 only (stateful, return auto). NACL: inbound TCP 22 **+ outbound ephemeral 1024–65535** (stateless).
- **C2.** Import script pattern (parameterized key name); run `./import.sh mykey ~/.ssh/aws.pub`; success `Imported 'mykey'.`; failure red `ERROR: File does not exist: /bad/path` (exit 1).
- **C3.** HTTP stateless = each request independent, server keeps no memory between requests. Stateful = remembers context (session/connection). Web apps fake state with **client-side cookies/tokens** resent each request.
- **C4.** SG is stateful → tracks connection → reply auto-allowed. NACL is stateless → no connection tracking → outbound reply to client **ephemeral port (1024–65535)** dropped. Fix: outbound NACL rule TCP 1024–65535 (and inbound 22 evaluated first).
- **C5.** (a) **Glacier Deep Archive** (cheapest, latency OK). (b) **FSx for Windows File Server** (SMB+AD). (c) **Storage Gateway — S3 File Gateway** (S3 as file share). (d) **FSx for Lustre** (HPC + S3). (e) **EBS** (boot volume).

---

# VERSION 2

## Section A — 20 select-all-that-apply (A–F)

**1.** Which are TRUE about **EC2**?
A. EBS volumes persist across an instance stop (when configured to).
B. Instance store data persists across a terminate.
C. In a key pair, AWS stores the public key and you store the private key.
D. An AMI packages the operating system.
E. A security group operates at the subnet level.
F. EC2 is an example of IaaS.

**2.** Which are TRUE about **EC2 pricing** scenarios?
A. Spot is appropriate for a batch job that tolerates interruption.
B. Reserved Instances suit a steady 24/7 workload.
C. On-Demand suits short, unpredictable workloads.
D. Spot is the best choice for a production database.
E. Reserved Instances require no commitment.
F. On-Demand provides the largest discount.

**3.** Which are TRUE about **deployment models**?
A. AWS is a public cloud.
B. On-premises + AWS together form a hybrid cloud.
C. A private cloud is dedicated to a single organization.
D. A community cloud is shared by organizations with similar needs.
E. On-premises always means private cloud.
F. A private cloud must be on-premises.

**4.** Which are TRUE about **IAM and the Shared Responsibility Model**?
A. AWS is responsible for physical data-center security.
B. The customer is responsible for patching the guest OS.
C. MFA is a form of authorization.
D. An IAM role provides temporary credentials.
E. An IAM user has long-term credentials.
F. The customer is responsible for securing the hypervisor.

**5.** Which CIDR blocks are **NOT allowed** for a VPC?
A. 0.0.0.0/8
B. 127.0.0.0/8
C. 169.254.0.0/16
D. 224.0.0.0/4
E. 10.0.0.0/8
F. 192.168.0.0/8

**6.** Which subnetting statements are TRUE?
A. /24 gives 256 total addresses.
B. /26 gives a 64-address block, 62 usable.
C. /28 gives 16 addresses, 14 usable.
D. /16 gives 65,536 addresses.
E. /30 gives 6 usable hosts.
F. Block size = 256 − (last octet of the mask).

**7.** Which are TRUE about **route tables, IGW, and NAT**?
A. `0.0.0.0/0` is the default route.
B. A public subnet has a route to an internet gateway.
C. A NAT gateway gives private subnets outbound internet.
D. An internet gateway attaches to a subnet.
E. A NAT gateway makes instances reachable from the internet.
F. A main route table is created automatically with the VPC.

**8.** Which are TRUE about **"Elastic"**?
A. An Elastic IP is a static public IP that can be remapped.
B. EBS Elastic Volumes resize without downtime.
C. EFS auto-scales to match demand.
D. "Elastic" means "free of charge."
E. "Elastic" means dynamically scalable/provisionable.
F. An Elastic IP is a private IPv4 address.

**9.** Which are TRUE about the **AWS CLI / JMESPath**?
A. `aws ec2 describe-key-pairs` = base / service / operation.
B. The default output is JSON.
C. `'KeyPairs[*].KeyName'` returns every key name.
D. `'sort_by(@, &CreateTime) | [-1].KeyName'` returns the newest key name.
E. `--output text` produces bare values.
F. You can omit `aws` and call `ec2` directly.

**10.** Which are TRUE about **Bash constructs**?
A. `$(command)` is command substitution.
B. `cat > f <<EOF … EOF` is a heredoc.
C. `[[ -f file ]]` tests that a file exists.
D. `$*` expands to all positional arguments.
E. `&>/dev/null` discards both stdout and stderr.
F. `>&2` writes to standard output.

**11.** Which are TRUE about **cloud-init**?
A. `write_files:` can set owner and permissions.
B. `runcmd:` commands run near the end of boot.
C. `packages:` installs software.
D. `users:` can inject SSH public keys.
E. cloud-init works only on AWS.
F. `cloud-init status --long` shows module status.

**12.** Which are TRUE about **S3 durability/security**?
A. S3 offers 11-nines durability.
B. S3 availability varies by storage class.
C. S3 One Zone-IA stores data in a single AZ.
D. Object Lock enables WORM (write-once-read-many).
E. S3 supports encryption in transit with SSL/TLS.
F. S3 Standard availability is 99.5%.

**13.** Which are TRUE about **S3 storage classes**?
A. Standard-IA is for infrequent access and charges retrieval fees.
B. Glacier Instant Retrieval offers millisecond retrieval.
C. Glacier Flexible Retrieval offers minutes-to-hours retrieval.
D. Glacier Deep Archive retrieval is 12–48 hours.
E. Intelligent-Tiering requires manual tier selection.
F. Express One Zone stores in a single AZ.

**14.** Which are TRUE about **EBS volume types**?
A. gp3 is a general-purpose SSD.
B. io2 is a provisioned-IOPS SSD for high-performance databases.
C. st1 is a throughput-optimized HDD for big data.
D. sc1 is the lowest-cost cold HDD.
E. gp2 cannot be used as a boot volume.
F. io2 Block Express supports Multi-Attach.

**15.** Which are TRUE about **protocols** (EFS / FSx / Gateway)?
A. EFS uses NFS 4.0/4.1.
B. FSx for Windows File Server uses SMB.
C. FSx for Lustre integrates with S3.
D. Volume Gateway uses iSCSI.
E. S3 File Gateway presents S3 via NFS/SMB.
F. EFS uses SMB.

**16.** Which are TRUE about **Storage Gateway types**?
A. S3 File Gateway presents S3 as a file share.
B. FSx File Gateway exposes FSx for Windows File Server.
C. Volume Gateway "cached" mode keeps primary data in S3.
D. Tape Gateway provides a virtual tape library.
E. Storage Gateway runs only as a physical appliance.
F. Volume Gateway "stored" mode keeps the full dataset on-premises.

**17.** Which are TRUE about **AWS Backup**?
A. It is policy-based.
B. Backups are KMS-encrypted by default.
C. It supports cross-region copies.
D. Backup vaults are immutable.
E. Backups are unencrypted by default.
F. It supports lifecycle transitions to cold storage.

**18.** A company needs a **shared file server with SMB and Active Directory permissions** for Windows clients. Which service is most appropriate?
A. Amazon S3
B. Amazon EBS
C. Amazon EFS
D. Amazon FSx for Windows File Server
E. AWS Storage Gateway — Tape Gateway
F. Amazon EBS io2

**19.** Which are correct **storage-category matchings**?
A. S3 — object storage
B. EBS — block storage
C. EFS — file storage
D. EBS — object storage
E. S3 — block storage
F. FSx — file storage

**20.** Which are TRUE about **regions/AZs and storage scope**?
A. A Region contains at least three AZs.
B. A VPC is regional.
C. A subnet is in a single AZ.
D. S3 Standard is multi-AZ.
E. EBS replicates within a single AZ.
F. A VPC spans a single AZ.

## Section B — 10 short-answer

1. What does "Elastic" mean, and why is EFS considered elastic?
2. Match object/block/file to S3/EBS/EFS.
3. Which S3 class for data accessed ~monthly but needed in milliseconds?
4. Explain the difference between gp3 and io2 (use case).
5. What is st1 optimized for?
6. EFS uses which protocol, and how many instances can share it?
7. FSx for Lustre targets what workload, and what does it integrate with?
8. Difference between Volume Gateway cached vs stored mode.
9. Compare S3 Standard availability vs One Zone-IA availability.
10. What does S3 Object Lock provide?

## Section C — Written response

**C1 (VPC).** You have VPC `172.31.0.0/16` in `us-east-1`. Design a three-tier setup (public web, private app, private DB), where only web is internet-reachable but app and DB can still fetch updates.
(a) Choose subnets (AZs + CIDRs).
(b) Draw/describe the route tables and their associations (which route goes where, incl. `0.0.0.0/0`).
(c) Explain the role of the NAT gateway and where it must live.
(d) A NACL on the web subnet allows TCP 443 inbound but HTTPS fails. What's missing and why?

**C2 (Bash).** Write a Bash script that finds the **most recent Debian 13 amd64 free-tier AMI ImageId** and writes it to a file as `debian_ami=<id>` using command substitution + heredoc. Show run command + sample output.

**C3 (Stateless — network).** Explain HTTP statelessness and how cookies/tokens simulate state. Contrast with a stateful protocol interaction.

**C4 (Stateless — VPC).** Explain why a security group needs only an inbound SSH rule, but a NACL needs two rules, using stateful/stateless and ephemeral ports.

**C5 (Storage scenario).** For each, name the service + one-sentence justification:
(a) Serve static website images and assets globally with caching.
(b) Mission-critical relational database needing 100k+ IOPS on a single instance.
(c) Shared storage for a fleet of Linux web servers mounting the same directory.
(d) Archive 10 years of compliance logs at minimum cost, retrieval in ~24h acceptable.
(e) Replace a physical tape library used by legacy backup software.

---

## VERSION 2 — Answer key

### Section A
1. **A, C, D, F.** B ✘ (instance store lost on terminate). E ✘ (SG is instance-level, not subnet).
2. **A, B, C.** D ✘ (Spot is interruptible — bad for DB). E ✘ (Reserved = commitment). F ✘ (Reserved discounts more).
3. **A, B, C, D.** E ✘ (on-prem ≠ private). F ✘ (private need not be on-prem).
4. **A, B, D, E.** C ✘ (MFA = authentication, not authorization). F ✘ (AWS secures hypervisor).
5. **A, B, C, D, E, F.** All are not allowed for a VPC: A–D are the blocked ranges; E (/8) and F (/8) exceed the /16 maximum. *(This is a "select all blocked" — every option is blocked.)*
6. **A, B, C, D, F.** E ✘ (/30 = 4 addresses, 2 usable).
7. **A, B, C, F.** D ✘ (IGW attaches to the VPC). E ✘ (NAT is outbound-only, not reachable from outside).
8. **A, B, C, E.** D ✘ (elastic ≠ free). F ✘ (EIP is public).
9. **A, B, C, D, E.** F ✘ (must use `aws`).
10. **A, B, C, D, E.** F ✘ (`>&2` writes stderr).
11. **A, B, C, D, F.** E ✘ (multi-cloud, not AWS-only).
12. **A, B, C, D, E.** F ✘ (Standard = 99.99%; 99.5% is One Zone-IA).
13. **A, B, C, D, F.** E ✘ (Intelligent-Tiering is automatic).
14. **A, B, C, D, F.** E ✘ (gp2 IS a boot volume).
15. **A, B, C, D, E.** F ✘ (EFS uses NFS).
16. **A, B, C, D, F.** E ✘ (runs as VM or EC2, not physical-only).
17. **A, B, C, D, F.** E ✘ (KMS by default).
18. **D.** FSx Windows File Server = SMB + AD. A ✘ (object). B ✘ (block, single instance). C ✘ (NFS, not SMB/AD). E ✘ (tape). F ✘ (block, not a file server).
19. **A, B, C, F.** D ✘ (EBS is block). E ✘ (S3 is object).
20. **A, B, C, D, E.** F ✘ (VPC spans region).

### Section B
1. Elastic = dynamically scales/provisions on demand without manual effort. EFS auto-scales to petabytes (grows/shrinks automatically).
2. Object → S3; Block → EBS; File → EFS.
3. **S3 Glacier Instant Retrieval** (millisecond retrieval for rarely-accessed data).
4. gp3 = general SSD (boot/dev, 3000 IOPS baseline); io2 = provisioned IOPS for mission-critical high-IOPS databases.
5. Throughput (MB/s) for big data / data warehouses.
6. NFS 4.0/4.1; multiple EC2 (and on-prem Linux) simultaneously.
7. HPC / big data; integrates with S3.
8. Cached: primary data in S3, hot data cached locally. Stored: full dataset on-prem, backups to S3.
9. Standard = 99.99%; One Zone-IA = 99.5% (single-AZ, lower availability).
10. WORM (write-once-read-many) immutability for compliance.

### Section C
- **C1.** (a) web `172.31.1.0/24` us-east-1a, app `172.31.2.0/24` us-east-1b, db `172.31.3.0/24` us-east-1c (all valid /24 subsets). (b) Public RT: `0.0.0.0/0 → IGW` associated with web subnet. App+DB RT: `0.0.0.0/0 → NAT` associated with app+db subnets. (c) NAT lives in the **public** subnet; gives app/db outbound-only internet. (d) NACL is stateless → needs an **outbound** rule for the return traffic (ephemeral ports 1024–65535).
- **C2.** `ami_id=$(aws ec2 describe-images --owners 136693071363 --filters … --query 'sort_by(Images,&CreationDate)[-1].ImageId' --output text)` then `cat > ami.txt <<EOF` writing `debian_ami=${ami_id}`; sample output `debian_ami=ami-0b3c68efb8f9567ef`.
- **C3.** Same as V1 C3.
- **C4.** Same as V1 C4.
- **C5.** (a) **S3 + CloudFront** (static + CDN caching). (b) **EBS io2** (high provisioned IOPS single instance). (c) **EFS** (shared NFS). (d) **S3 Glacier Deep Archive** (cheapest, 12–48h OK). (e) **Storage Gateway — Tape Gateway** (virtual tape library).

---

# VERSION 3

## Section A — 20 select-all-that-apply (A–F)

**1.** Which are TRUE about **EC2**?
A. An instance type defines CPU/memory/storage/network configuration.
B. An AMI is a preconfigured template.
C. EBS is persistent block storage.
D. Instance store is ephemeral.
E. A security group is a stateful instance-level firewall.
F. AWS stores the private key of a key pair.

**2.** Which are TRUE about **EC2 pricing**?
A. Reserved Instances are typically 1–3 year commitments.
B. Spot instances can be up to ~90% cheaper.
C. Spot instances can be reclaimed by AWS.
D. On-Demand is billed per second (or hour).
E. Reserved Instances never provide a discount.
F. Spot is appropriate for fault-tolerant, interruptible workloads.

**3.** Which are TRUE about **service & deployment models**?
A. SaaS delivers a full application stack as a service.
B. PaaS lets you focus on app development, not infrastructure.
C. IaaS gives the highest level of control.
D. A public cloud is run by a third-party provider.
E. A community cloud is dedicated to one organization.
F. Hybrid combines public and private clouds.

**4.** Which are TRUE about **IAM and the Shared Responsibility Model**?
A. A group lets you attach policies to many users at once.
B. A role is assumed to obtain temporary credentials.
C. The customer is responsible for physical data-center security.
D. AWS is responsible for hardware security.
E. Least privilege means granting minimum necessary permissions.
F. The root user should have MFA enabled.

**5.** Which are TRUE about **RFC 1918 ranges**?
A. 10.0.0.0/8 is a private range.
B. 172.16.0.0/12 is a private range.
C. 192.168.0.0/16 is a private range.
D. 172.31.0.0/16 falls inside 172.16.0.0/12.
E. 169.254.0.0/16 is an RFC 1918 private range.
F. 224.0.0.0/4 is an RFC 1918 private range.

**6.** Which are TRUE about **usable hosts**?
A. /24 → 254 usable.
B. /26 → 62 usable.
C. /28 → 14 usable.
D. /30 → 2 usable.
E. /16 → 65,534 usable.
F. /28 → 16 usable.

**7.** Which are TRUE about **security group & NACL defaults**?
A. A new security group has no inbound rules.
B. A new security group allows all outbound traffic.
C. A default NACL allows all inbound and outbound traffic.
D. A security group supports deny rules.
E. NACL rules are evaluated lowest-number first.
F. A security group is stateless.

**8.** Which are TRUE about **"Elastic"**?
A. Elastic IP is an AWS service name.
B. Elastic Block Store is an AWS service name.
C. Elastic File System is an AWS service name.
D. "Elastic" implies auto-scaling/dynamic provisioning.
E. EC2 stands for "Elastic Compute Cloud."
F. "Elastic" means "free of charge."

**9.** Which are TRUE about the **AWS CLI**?
A. `fileb://` reads raw binary (use for SSH keys).
B. `--query` uses JMESPath.
C. `describe-images --filters` narrows the result set.
D. `--owners 136693071363` is Debian's account ID.
E. `aws login --remote` is used inside a VM.
F. The default output format is YAML.

**10.** Which are TRUE about **Bash error handling**?
A. `set -e` exits on error.
B. `exit 1` signals failure.
C. `>&2` writes to stderr.
D. `$#` is the argument count.
E. `[[ ! -f "$1" ]]` tests that a file does NOT exist.
F. `&>/dev/null` shows output on screen.

**11.** Which are TRUE about **cloud-init modules**?
A. `users:` creates users and injects SSH keys.
B. `packages:` installs packages.
C. `write_files:` writes files.
D. `runcmd:` runs commands.
E. `systemctl enable/restart nginx` is typical in `runcmd:`.
F. cloud-init works only on Windows.

**12.** Which are TRUE about **S3 use cases**?
A. Static website hosting.
B. Data lake for analytics.
C. Backup target.
D. Triggering Lambda on upload.
E. Root filesystem for an EC2 instance.
F. Media distribution.

**13.** Which are TRUE about **S3 retrieval times**?
A. S3 Standard — immediate.
B. Glacier Instant Retrieval — milliseconds.
C. Glacier Flexible Retrieval — minutes to hours.
D. Glacier Deep Archive — 12–48 hours.
E. One Zone-IA — multi-AZ.
F. Standard-IA — charges retrieval fees.

**14.** Which are TRUE about **EBS features**?
A. Snapshots are point-in-time.
B. Snapshots are incremental.
C. Elastic Volumes resize without downtime.
D. Multi-Attach (io2 Block Express) requires instances in the same AZ.
E. EBS replicates across AZs by default.
F. EBS supports AES-256 encryption via KMS.

**15.** Which are TRUE about **EFS**?
A. Uses NFS.
B. Is regional (multi-AZ).
C. Offers 11-nines durability.
D. Auto-scales to petabytes.
E. Access points enforce POSIX permissions.
F. Is object storage.

**16.** Which are TRUE about **FSx**?
A. FSx for Windows File Server uses SMB + Active Directory.
B. FSx for Lustre targets HPC.
C. FSx for NetApp ONTAP supports multiprotocol (NFS/SMB/iSCSI).
D. FSx for OpenZFS provides ZFS.
E. FSx is object storage.
F. FSx for Lustre integrates with S3.

**17.** Which are TRUE about **Storage Gateway deployment**?
A. Can run as a VMware VM.
B. Can run on Hyper-V.
C. Can run on KVM.
D. Can run as an EC2 instance.
E. Runs only as a physical appliance.
F. Caches frequently accessed data locally.

**18.** A company must keep **7 years of legal records at minimum cost**, retrieval within a day is acceptable. Which service is most appropriate?
A. S3 Standard
B. S3 Standard-IA
C. S3 Glacier Deep Archive
D. EBS sc1
E. EFS Archive
F. S3 Glacier Instant Retrieval

**19.** A single EC2 instance runs a **mission-critical database needing 100,000+ IOPS with sub-ms latency**. Which volume is most appropriate?
A. EBS gp3
B. EBS io2
C. EFS
D. S3
E. EBS st1
F. FSx for Lustre

**20.** Which are TRUE about **regions/AZs**?
A. A Region contains multiple Availability Zones.
B. Each Region has at least three AZs.
C. A VPC is regional.
D. A subnet is in a single AZ.
E. An AZ is an isolated location within a Region.
F. A Region contains exactly one AZ.

## Section B — 10 short-answer

1. What does "Elastic" mean, and why is EFS (Elastic File System) elastic?
2. Name four S3 storage classes and one distinguishing word each.
3. gp3 vs io2: when would you choose each?
4. st1 vs sc1: when would you choose each?
5. What is the scope (AZ/region) of EBS Multi-Attach?
6. EFS protocol and concurrency (how many instances).
7. FSx for Windows File Server protocol + AD.
8. What problem does Tape Gateway solve?
9. Durability vs availability (one sentence each).
10. Which service for a single EC2 boot volume, and why?

## Section C — Written response

**C1 (VPC).** VPC `192.168.0.0/16` in `ca-central-1`. Design a public web + private DB tier, and explain how to add a bastion host for admin SSH into the private tier.
(a) Subnets (AZs + CIDRs).
(b) Route tables + associations + IGW.
(c) How the DB reaches the internet for updates (name the resource, where it lives).
(d) For SSH into the DB via the bastion, which security groups need which rules (stateful) — and what extra rules would NACLs need?

**C2 (Bash).** Write a Bash script that imports an SSH key, validating the argument, detecting duplicates, and handling errors with a red message + exit 1. Show run command + sample success/failure output.

**C3 (Stateless — network).** Define stateless vs stateful at the protocol level and explain how HTTP (stateless) apps maintain sessions.

**C4 (Stateless — VPC).** Explain why a NACL allowing only inbound TCP 22 breaks SSH, while a security group with the same rule works. Include ephemeral ports.

**C5 (Storage scenario).** For each, name the service + one-sentence justification:
(a) Shared file storage for Linux servers using NFS that scales automatically.
(b) Lowest-cost, rarely-accessed archive with 12–48h retrieval.
(c) Windows department file server with AD.
(d) On-prem apps that need block storage backed by S3.
(e) Centralized backups across EC2, RDS, and DynamoDB.

---

## VERSION 3 — Answer key

### Section A
1. **A, B, C, D, E.** F ✘ (AWS stores public; you store private).
2. **A, B, C, D, F.** E ✘ (Reserved does discount).
3. **A, B, C, D, F.** E ✘ (community = shared by similar orgs).
4. **A, B, D, E, F.** C ✘ (AWS, not customer, secures physical DC).
5. **A, B, C, D.** E ✘ (link-local, not RFC 1918). F ✘ (multicast, not RFC 1918).
6. **A, B, C, D, E.** F ✘ (/28 = 16 total, 14 usable).
7. **A, B, C, E.** D ✘ (SG is allow-only). F ✘ (SG is stateful).
8. **A, B, C, D, E.** F ✘ (elastic ≠ free).
9. **A, B, C, D, E.** F ✘ (default is JSON).
10. **A, B, C, D, E.** F ✘ (`&>/dev/null` hides output).
11. **A, B, C, D, E.** F ✘ (multi-platform, Linux-focused).
12. **A, B, C, D, F.** E ✘ (S3 is not a root filesystem).
13. **A, B, C, D, F.** E ✘ (One Zone-IA is single-AZ).
14. **A, B, C, D, F.** E ✘ (EBS is single-AZ by default).
15. **A, B, C, D, E.** F ✘ (EFS is file storage).
16. **A, B, C, D, F.** E ✘ (FSx is file storage).
17. **A, B, C, D, F.** E ✘ (not physical-only).
18. **C.** Deep Archive = cheapest, 12–48h OK. A ✘ (active, expensive). B ✘ (IA, higher cost than archive). D ✘ (block HDD, not object archive). E ✘ (EFS Archive exists but file storage, not the cheapest archive). F ✘ (Instant Retrieval is pricier than Deep Archive).
19. **B.** io2 = provisioned IOPS, sub-ms, high IOPS. A ✘ (gp3 caps lower). C ✘ (shared file, not single-instance block). D ✘ (object). E ✘ (HDD, low IOPS). F ✘ (HPC file system).
20. **A, B, C, D, E.** F ✘ (Region has multiple AZs).

### Section B
1. Elastic = dynamically scales/provisions on demand. EFS auto-scales to petabytes.
2. Standard (frequent/default), Standard-IA (infrequent), Glacier Deep Archive (cheapest), Glacier Instant Retrieval (millisecond). *(any 4 valid)*
3. gp3 = general/boot (3,000 IOPS baseline, cheaper); io2 = provisioned high IOPS for mission-critical DBs.
4. st1 = throughput-optimized (big data/warehouse); sc1 = cold, lowest-cost HDD (infrequent).
5. Same AZ only (io2 Block Express).
6. NFS 4.0/4.1; multiple instances.
7. SMB; Active Directory.
8. Replaces physical tape libraries with a virtual tape library backed by S3/Glacier.
9. Durability = probability data isn't lost (11 nines); availability = % of time service is reachable (99.99%).
10. EBS (block boot volume); EFS is shared file (wrong role), S3 is object (not a root FS).

### Section C
- **C1.** (a) web `192.168.1.0/24` ca-central-1a, db `192.168.2.0/24` ca-central-1b. (b) IGW → attach VPC → `0.0.0.0/0 → IGW` on web's route table; db's route table → `0.0.0.0/0 → NAT`. (c) **NAT gateway** in the public subnet. (d) Bastion SG: inbound SSH from your IP (stateful). DB SG: inbound SSH **only from the bastion's SG**. NACLs would additionally need outbound ephemeral-port rules (stateless).
- **C2.** Import-key script (validate `$#`, `[[ ! -f ]]`, duplicate check, `fileb://`, `err()` red + exit 1). Run `./import.sh mykey ~/.ssh/aws.pub`; success `Imported 'mykey'.`; failure red `ERROR: ...`.
- **C3.** Stateless = each request independent, no server memory; stateful = remembers context. HTTP apps use cookies/tokens to simulate state.
- **C4.** SG stateful → reply auto-allowed. NACL stateless → needs outbound ephemeral (1024–65535) rule; missing rule drops the reply.
- **C5.** (a) **EFS** (shared NFS, auto-scale). (b) **S3 Glacier Deep Archive** (cheapest). (c) **FSx for Windows File Server** (SMB+AD). (d) **Storage Gateway — Volume Gateway** (iSCSI block backed by S3). (e) **AWS Backup** (centralized multi-service backup).

---

*End. Attempt all three closed-book, spaced at least a day apart, and re-derive (don't re-read) the SG-vs-NACL rule and the storage-paradigm map each time.*
