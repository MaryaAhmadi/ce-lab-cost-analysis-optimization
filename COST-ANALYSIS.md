# Week 2 AWS Cost Analysis

## EC2 Instances

| InstanceId           | InstanceType | State   | PublicIpAddress |
|---------------------|-------------|---------|----------------|
| i-02ff2d33c91eefa8d | t3.small    | stopped | None           |

## EBS Volumes

| VolumeId              | Size (GB) | State  | VolumeType |
|----------------------|-----------|--------|------------|
| vol-03cfd68d751dafdb9 | 8        | in-use | gp3        |
| vol-0bf19ce1fe0db2f36 | 8        | in-use | gp3        |

## Current Costs

| Resource          | Type     | Hours | Weekly Cost | Monthly Cost |
|------------------|---------|-------|------------|--------------|
| EC2 i-02ff2d33c91eefa8d | t3.small | stopped | $0        | $0           |
| EBS vol-03cfd68d751dafdb9 | gp3 8GB | N/A   | $0.16     | $0.64        |
| EBS vol-0bf19ce1fe0db2f36 | gp3 8GB | N/A   | $0.16     | $0.64        |

**Total Weekly Cost:** ~$0.32  
**Total Monthly Cost:** ~$1.28
