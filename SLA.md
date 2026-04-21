### SLI v/s SLO v/s SLA

SLIs (Service Level Indicators) measure actual performance (e.g., latency), SLOs (Service Level Objectives) set internal targets for those metrics (e.g., 99.9% uptime), and SLAs (Service Level Agreements) are formal, legal contracts with customers promising specific performance levels with consequences.

### SLI (Service Level Indicator): The Metric

The actual measurement of a service's performance.

Examples: Error rate, application latency, system throughput, or uptime percentage.

Purpose: Provides data on how the system is currently behaving.

### SLO (Service Level Objective): The Target 

The target value or range of values for an SLI.

Examples: 99.9% of requests successful (over 30 days), or 95% of requests served in under 100ms.

Purpose: Defines "acceptable" reliability and creates error budgets to guide engineering teams. 

### SLA (Service Level Agreement): The Contract 

A legal agreement with a customer that outlines responsibilities, including metrics, targets, and penalties.

Examples: "If service uptime falls below 99.5%, customer receives 10% credit".

Purpose: Ensures business compliance and defines the consequence of failure.