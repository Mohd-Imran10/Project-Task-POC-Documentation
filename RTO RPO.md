### 1. RTO (Recovery Time Objective)

RTO is the maximum acceptable time a system can be down after a failure or disaster. It defines how quickly services must be restored to avoid major business impact. A lower RTO means faster recovery is required, often needing automation and backup systems. It focuses on time to recover operations.

Example:
If RTO = 1 hour → the system must be back online within 1 hour after failure.

### 2. RPO (Recovery Point Objective)

RPO is the maximum acceptable data loss measured in time. It defines how much recent data the system can afford to lose during a failure. A lower RPO requires frequent backups or real-time replication. It focuses on how much data can be lost.

Example:
If RPO = 15 minutes → you can only lose up to 15 minutes of data.

### 3. Key Difference
RTO → How fast you recover (time)
RPO → How much data you can lose (data loss window)


### 4. Real-Time Example (E-commerce)

RTO = 2 hours → Website must be restored within 2 hours after outage

RPO = 10 minutes → Maximum 10 minutes of order data can be lost