# AWS Cost Optimization Plan – Week 2

## Current State
- Total monthly cost: $1.28
- Instances: 1 stopped
- EBS Volumes: 2 in-use
- Average utilization: ~5% (t3.small)

## Identified Optimizations

| Opportunity        | Found                        | Optimization                  | Savings          |
|-------------------|------------------------------|-------------------------------|----------------|
| Stop/Terminate    | 1 stopped instance           | Terminate if not needed       | ~$0.64/month    |
| Right-size        | t3.small low CPU usage       | Downgrade to t3.micro         | ~$0.64/month    |
| Reserved Pricing  | Running >6 months predicted  | 1-year Reserved Instance      | ~$180/year      |

## Implementation Priority
1. Quick wins (this week)
   - Terminate stopped instance
2. Medium-term (this month)
   - Right-size instance
3. Long-term
   - Reserved instance planning

## Projected Savings
- Total Monthly: ~$1.28 → ~$0.64/month (≈50% reduction)
- Annual: ~$7.68/year



Right-size web server
   - Found: t3.small with 5% average CPU utilization
   - Optimization: Downgrade to t3.micro
   - Savings: ~$15/month (≈50% reduction)


# Example CLI commands (replace with real instance IDs)

aws ec2 stop-instances --instance-ids <INSTANCE_ID>
aws ec2 modify-instance-attribute --instance-id <INSTANCE_ID> --instance-type "{\"Value\": \"t3.micro\"}"
aws ec2 start-instances --instance-ids <INSTANCE_ID>


Reserved Instance
   - Found: Instance runs 24/7 predicted for >6 months
   - Optimization: Purchase 1-year Reserved Instance
   - Savings: ~$180/year (≈50% reduction)




# Pseudocode Lambda to stop dev instances at 6 PM weekdays
import boto3
ec2 = boto3.client('ec2')
instances_to_stop = ['i-xxxxx']  # replace with instance IDs
ec2.stop_instances(InstanceIds=instances_to_stop)



