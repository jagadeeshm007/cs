---
tags: [infra, cloud, aws]
phase: 4
---
# ☁️ Cloud (AWS-first; concepts map to GCP/Azure)

## Core services to know well
| Area | AWS | GCP equivalent |
|---|---|---|
| Identity | **IAM** (users, roles, policies, least privilege), STS | IAM |
| Network | **VPC**, subnets (public/private), route tables, NAT GW, security groups, NACLs, PrivateLink | VPC |
| Compute | EC2, **ECS/Fargate**, **EKS**, Lambda | GCE, Cloud Run, GKE, Cloud Functions |
| Storage | **S3** (classes, lifecycle, presigned URLs), EBS, EFS | GCS |
| Database | **RDS/Aurora Postgres**, DynamoDB, ElastiCache/MemoryDB (Valkey/Redis) | Cloud SQL, Spanner, Firestore, Memorystore |
| Messaging | SQS, SNS, EventBridge, **MSK** (Kafka), Kinesis | Pub/Sub |
| Edge | CloudFront, Route 53, ALB/NLB, API Gateway, WAF | Cloud CDN, Cloud LB |
| Observability | CloudWatch, X-Ray | Cloud Monitoring |
| Secrets | Secrets Manager, KMS, Parameter Store | Secret Manager, KMS |
| AI | **Bedrock**, SageMaker | Vertex AI |

## Concepts
- [ ] Regions, AZs, the shared responsibility model
- [ ] Well-Architected Framework (6 pillars) ⭐
- [ ] High availability across AZs; DR strategies (backup/restore, pilot light, warm standby, multi-site)
- [ ] Cost: on-demand vs reserved vs spot, egress costs, NAT gateway costs (a classic surprise bill)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Budget alerts first; LocalStack for S3/SQS locally
- [ ] 🟡 S3 presigned uploads (valet key) for knowledge docs
- [ ] 🔴 Deploy Orbit to k3s-on-EC2 or EKS with RDS + S3 via Terraform; **destroy after**
- [ ] ⚫ Bedrock as an extra provider in the LLM gateway (IAM auth)

## 🧠 Cognitive tasks
- [ ] Fermi: the monthly AWS bill for Orbit at 1,000 tenants; find the NAT gateway surprise

## 🛰️ Orbit integration
- [ ] The Phase 4 Production Day boss fight

> [!info] Go deeper
> 🧩 [[Distributed & Cloud Patterns]]

## Certification (optional, useful for the resume)
AWS Certified Solutions Architect – Associate (SAA-C03). Adrian Cantrill's course or Stephane Maarek's.

## Resources
- AWS docs · **AWS Builders' Library** ⭐ (excellent distributed systems articles) · AWS Well-Architected
