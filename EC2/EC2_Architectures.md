# AWS Production Architecture (Full Stack)

```mermaid
flowchart TB
    %% User Access
    Users[Users / Internet]

    %% DNS & Edge
    Route53[Route 53 DNS]
    CloudFront[CloudFront CDN + Edge Caching]
    Shield[AWS Shield (DDoS Protection)]
    WAF[AWS WAF (Web Application Firewall)]

    %% Load Balancer & SSL
    ALB[Application Load Balancer (HTTPS)]
    ACM[ACM Certificate]

    %% VPC and Subnets
    subgraph VPC[ VPC (10.0.0.0/16) ]
        subgraph Public[Public Subnets (Multi-AZ)]
            ALB
        end

        subgraph PrivateAZ1[Private Subnet AZ1]
            EC2_1[EC2 Auto Scaling Group]
        end
        subgraph PrivateAZ2[Private Subnet AZ2]
            EC2_2[EC2 Auto Scaling Group]
        end

        %% Database
        subgraph DB[Database Layer]
            RDS_Primary[RDS Primary (Multi-AZ, Encrypted)]
            RDS_Replica[RDS Read Replica (Optional)]
        end

        %% Storage & Backup
        S3[S3 (Static Assets, Logs, Backups)]
        EBS[EBS Volumes (Encrypted)]
    end

    %% Monitoring & Security
    CloudWatch[CloudWatch (Monitoring & Logs)]
    CloudTrail[CloudTrail (Audit Logs)]
    Config[AWS Config (Compliance)]
    SystemsManager[AWS Systems Manager]
    IAM[IAM Roles]

    %% Connections
    Users --> Route53 --> CloudFront --> Shield --> WAF --> ALB
    ALB --> EC2_1
    ALB --> EC2_2
    EC2_1 --> EBS
    EC2_2 --> EBS
    EC2_1 --> RDS_Primary
    EC2_2 --> RDS_Replica
    RDS_Primary --> S3
    RDS_Replica --> S3
    EC2_1 --> CloudWatch
    EC2_2 --> CloudWatch
    EC2_1 --> SystemsManager
    EC2_2 --> SystemsManager
    EC2_1 --> IAM
    EC2_2 --> IAM
    RDS_Primary --> CloudTrail
    RDS_Replica --> CloudTrail
    ALB --> ACM