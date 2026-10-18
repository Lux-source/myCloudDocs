# myCloudDocs
Hi! This is myCloudDocs, my personal space for sharing documentation on cloud projects and web deployment. It's where I keep the practical stuff – guides, tips, and how-tos – from my hands-on experiences with AWS and Azure. I hope you find these docs helpful!

## Guides

| Name | Description | Link |
|------|-------------|------|
| 3-Tier Web Application | Three tier architecture, ELB, integration with S3, RDS (PostgreSQL engine), VPC, EC2. | https://lucians-docs.gitbook.io/multi-tier-web-application-deployment/ | 
| Serverless Data Processing Pipepline on AWS | Serverless architecture, event-driven programming, integration with S3, Lambda and DynamoDB. | https://lucians-docs.gitbook.io/serverless-data-processing-pipeline-on-aws/ | 
| WordPress Hosted on AWS | Security group configurations, Aurora RDS integration and Deployment Workflow on AWS. | https://lucians-docs.gitbook.io/wordpress-site-deployment-on-amazon-ec2/ |

## Container migration playbooks

How each app on my [portfolio](https://lucianandreinegoita.dev/) moves to containers on Kubernetes, with the AWS (EKS) and Azure (AKS) designs side by side, diagrams, the code changes each app needs first, data migration steps and risks. Start with the [overview](migrations/README.md).

| Playbook | What it covers |
|---|---|
| [Platform: AWS](migrations/platform-aws.md) | EKS landing zone: VPC, Gateway API on ALB, Pod Identity, Secrets Manager, Argo CD, observability |
| [Platform: Azure](migrations/platform-azure.md) | AKS landing zone: private endpoints, Application Gateway for Containers, Workload ID, Key Vault |
| [Mortgage Analyst](migrations/apps/mortgage-analyst.md) | Spring Boot + PostgreSQL, scheduled jobs moved to CronJobs, Liquibase as a pre-deploy Job |
| [LucyERP](migrations/apps/lucyerp.md) | From an on-premise SQLite install to a multi-tenant deployment on PostgreSQL |
| [Relay Traffic Copilot](migrations/apps/relay-copilot.md) | A six-thread Python process split into a web Deployment and CronJobs |
| [peaje](migrations/apps/peaje.md) | A single-writer Go ledger: StatefulSet on block storage, and the path to scale out |
| [Collaborative editor (thesis)](migrations/apps/collaborative-editor.md) | Moodle, Hocuspocus and Kafka: shared storage, Redis, MSK and Event Hubs |
| [Reference manifests](migrations/examples/mortgage-analyst/) | Kustomize base with AWS and Azure overlays, validated with kubeconform |
