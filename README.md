# ShopPro International – Cloud Migration Cost Report

Cloud Migration (CST8913) – Lab 09 | November 2026

Student: Justin

## 1. Cost Estimate Report

I used the Microsoft Azure Pricing Calculator to estimate the infrastructure for ShopPro International. The figures below come from my exported Azure estimate and are in US dollars. The estimate is a planning exercise, not an invoice or a complete production quote.

Azure estimated monthly cost: $25,088.70. Azure estimated annual cost: $301,064.36. The calculator displays $0.00 upfront because one-time migration work was not priced in the export. The monthly amount includes the configurations below.

| Azure item | Configuration | USD/month |
| --- | --- | --- |
| Front-end – North America | 10 Linux VMs, East US | 847.90 |
| Front-end – Europe | 10 Linux VMs, West Europe | 1,008.50 |
| Front-end – Asia-Pacific | 10 Linux VMs, Southeast Asia | 972.00 |
| API services | 20 Linux VMs, East US; capacity for 50 microservices | 2,803.20 |
| Payments | 3 Windows VMs, East US | 1,284.24 |
| Primary database | Azure SQL Database, approximately 5 TB | 2,018.17 |
| NoSQL database | Azure Cosmos DB, approximately 10 TB | 3,728.00 |
| Load balancing | One Standard Load Balancer, East US | 23.25 |
| Data warehouse | Azure Synapse Analytics; 15 TB storage assumption | 7,546.62 |
| Machine learning | 2 GPU VMs, 160 hours/month | 168.32 |
| Monitoring | Azure Monitor, log ingestion assumption | 3,438.50 |
| Disaster recovery | Azure Site Recovery, 50 protected instances | 1,250.00 |
| TOTAL | Current Azure estimate | 25,088.70 |

The monthly line items add to $25,088.70. The exported annual total is $301,064.36; multiplying the displayed rounded monthly figure by 12 gives $301,064.40, a $0.04 rounding difference.

### One-time migration estimate (planning assumptions)

The professor asks for data transfer, replication and temporary migration resources. They are not priced in the Azure export, so I used a separate illustrative planning allowance below. These amounts are assumptions, not Azure calculator prices.

| Migration item | Assumption | One-time USD |
| --- | --- | --- |
| Temporary migration VMs | 4 VMs × $150/month × 2 months | 1,200 |
| Staging and replication storage | 20 TB × $25/TB/month × 2 months | 1,000 |
| Database replication and cutover | Tooling and transfer allowance | 2,000 |
| Initial data transfer/network | Transfer allowance, verify inbound/egress pricing | 1,000 |
| Testing and migration support | 80 hours × $75/hour | 6,000 |
| TOTAL | Illustrative one-time allowance | 11,200 |

The migration allowance is $11,200, separate from recurring Azure costs. Actual transfer costs, software licensing, downtime, staffing and database migration tools must be confirmed after assessment. Azure Migrate can support discovery and planning, but not all related resources are free.

### Operating and management costs

The VM, database, warehouse, GPU and load-balancer lines represent the operating estimate. Azure Monitor ($3,438.50/month) and Site Recovery ($1,250/month) are the main separately priced management/recovery services. Microsoft Cost Management budgets and resource tags should be used to track spending by region, application and team.

Important limitations: this export does not separately price Azure Front Door/CDN, load balancers in Europe and Asia, full network egress, all backup storage, Microsoft Defender for Cloud, PCI DSS assessment and security tooling, container orchestration, or the complete regional failover environment. The 20 backend VMs are in East US, so the current quote does not establish full three-region backend availability. These costs must be added before a production budget is approved.

## 2. Cost Optimization Strategy

I would keep pay-as-you-go as the baseline and compare one-year and three-year commitments for workloads that stay online. Reservations can save money but reduce flexibility. I would avoid reserving the GPU training VMs because they run only 160 hours a month.

Example reservation comparison: the 30 front-end and 20 API VMs cost $5,631.60/month in the current estimate, including disks. For a simple comparison, if the eligible amount received a 20% one-year reduction, the illustrative saving would be $1,126.32/month. At 35% for three years, it would be $1,971.06/month. These percentages are assumptions applied to the full line items, not actual Azure reserved quotes; real discounts usually apply to eligible compute only, not disks, and must be checked in the calculator.

For autoscaling, I would use a smaller number of front-end and API instances off-peak and scale out during shopping peaks. As an example, reducing eligible compute usage by 20% during half of the month could lower that portion of usage by about 10% overall. Actual savings depend on minimum capacity, utilization and whether the service can scale down safely.

I would also right-size VMs after monitoring CPU and memory, stop unused test environments, run GPU and batch jobs on a schedule, pause Synapse compute when possible, and use storage lifecycle rules. Azure Hybrid Benefit should only be included if ShopPro owns eligible Windows Server or SQL Server licenses. For payments, encryption in transit and at rest, restricted access, auditing, network segmentation and PCI DSS validation remain necessary even if they increase cost.

## 3. Future Growth and Budget Plan

For a simple three-year plan, I assumed annual demand growth of 15% and annual optimization of 5%. I applied both factors each year (1.15 × 0.95 = 1.0925). These are my assumptions and are not forecasts from Microsoft.

| Year | Monthly operating USD | Annual operating USD |
| --- | --- | --- |
| Year 1 | 25,088.70 | 301,064.36 |
| Year 2 | 27,409.40 | 328,912.82 |
| Year 3 | 29,944.77 | 359,337.25 |

Three-year operating total: $989,314.43. Adding the illustrative $11,200 migration allowance gives $1,000,514.43 over three years, before the missing services, taxes and any additional regional expansion.

To control future costs, ShopPro should review budgets monthly and forecasts quarterly, introduce reserved pricing only for stable demand, adopt newer VM families after testing, use serverless services for intermittent tasks, and track spending with tags for region and workload. The company should also test backups and recovery in each region before migration is considered complete.

## Conclusion and sources

Azure can support ShopPro’s migration, but the current calculator estimate is only a partial baseline. I would first complete the missing CDN, security, backup and network estimates, then test performance, migration and disaster recovery before committing to a final budget.

Sources: Microsoft Azure Pricing Calculator, ExportedEstimate.xlsx (November 2026); ShopPro International Lab 09 scenario. Migration allowances, reservation examples and growth assumptions are my own planning examples and are identified as such.

[Estimation_Cloud_Migrantion9.docx](Estimation_Cloud_Migrantion9.docx)

[ExportedEstimate.xlsx](ExportedEstimate.xlsx)
