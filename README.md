# Lab M2.10 - Cost Analysis and Optimization

**Repository:** [https://github.com/cloud-engineering-bootcamp/ce-lab-cost-analysis-optimization](https://github.com/cloud-engineering-bootcamp/ce-lab-cost-analysis-optimization)

**Activity Type:** Individual  
**Estimated Time:** 30-45 minutes

## Learning Objectives

- [ ] Use AWS Cost Explorer to analyze spending
- [ ] Calculate costs for different configurations
- [ ] Identify optimization opportunities
- [ ] Create cost optimization plan
- [ ] Implement cost-saving measures

## Your Task

Analyze your Week 2 AWS usage and create optimization plan:
1. Review Cost Explorer for EC2 costs
2. Calculate actual vs potential costs
3. Identify specific optimizations
4. Implement at least 2 optimizations
5. Project savings

**Success:** Cost optimization plan saving ≥30%

## Cost Analysis Steps

### 1. Gather Current Configuration

```bash
# List all your instances
aws ec2 describe-instances \
  --filters "Name=tag:Project,Values=CloudBootcamp" \
  --query 'Reservations[].Instances[].[InstanceId,InstanceType,State.Name,PublicIpAddress]' \
  --output table

# List EBS volumes
aws ec2 describe-volumes \
  --filters "Name=tag:Project,Values=CloudBootcamp" \
  --query 'Volumes[].[VolumeId,Size,State,VolumeType]' \
  --output table

# List unattached volumes (waste!)
aws ec2 describe-volumes \
  --filters "Name=status,Values=available" \
  --query 'Volumes[].[VolumeId,Size,CreateTime]' \
  --output table
```

### 2. Calculate Current Costs

```
Instance 1: t3.micro running 168 hours this week
  168 hours × $0.0104/hour = $1.75

Instance 2: t3.small running 120 hours this week
  120 hours × $0.0208/hour = $2.50

EBS: 3 volumes × 8 GB × $0.08/GB/month = $1.92/month

Total Week 2 costs: ~$4.25
Projected monthly (4 weeks): ~$17
```

### 3. Optimization Opportunities

**Opportunity 1: Stop unused instances**
```
Found: 1 instance stopped but not terminated
Optimization: Terminate if not needed
Savings: $0.64/month (EBS storage)
```

**Opportunity 2: Right-size**
```
Found: t3.small with 5% average CPU
Optimization: Downgrade to t3.micro
Savings: $15/month (50% reduction)
```

**Opportunity 3: Reserved pricing**
```
Found: Instance runs 24/7 for >6 months predicted
Optimization: 1-year Reserved Instance
Savings: ~$180/year (50% savings)
```

### 4. Create Optimization Plan

**Template:**
```markdown
# Cost Optimization Plan

## Current State
- Total monthly cost: $XXX
- Instances: X running, Y stopped
- Average utilization: XX%

## Identified Optimizations
1. Stop dev instances overnight
   - Savings: $XX/month
2. Right-size web server
   - Savings: $XX/month
3. Delete unattached volumes
   - Savings: $XX/month

## Implementation Priority
1. Quick wins (this week)
2. Medium term (this month)
3. Long term (planning)

## Projected Savings
- Total: $XX/month (XX% reduction)
- Annual: $XXX/year
```

### 5. Implement Optimizations

```bash
# Terminate unused instances
aws ec2 terminate-instances --instance-ids i-xxxxx

# Delete unattached volumes
aws ec2 delete-volume --volume-id vol-xxxxx

# Create stop schedule (pseudocode)
# Lambda function to stop instances at 6 PM weekdays
```

## 📤 What to Submit

**Submission Type:** GitHub Repository

Create a **public** GitHub repository named `ce-lab-cost-optimization` containing:
- `COST-ANALYSIS.md` - Current costs
- `OPTIMIZATION-PLAN.md` - Your plan
- `cost-calculator.xlsx` or `.csv` - Calculations
- `implementation-log.md` - What you changed
- Screenshots of Cost Explorer
- Projected savings report

## Bonus

- Set up budget alert at $50/month
- Create cost allocation tags
- Compare Reserved vs On-Demand savings

## Grading: 100 points
- Cost analysis accuracy: 25pts
- Optimization identification: 25pts
- Implementation: 25pts
- Documentation: 15pts
- Projected savings: 10pts
