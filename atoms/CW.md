CloudWatch is an #AWSService that provides system-wide visibility into resource utilization, application performance, and operational health for every service. 

It is a metrics repository. Supports Logs, Metrics, and Alarms.
See: [CW UG](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)

---

#Question What API can be used for metrics?
- Use `PutMetricData --timestamp` with optional `StorageResolution` : 1, 5, 10, 30-second intervals (expensive). 
- Accepts metric data points two weeks in the past and 2 hours in the future.
- High-resolution custom metrics and alarms support 1-second metrics

![[CloudWatch Metrics Alarms Notifications Actions Architecture.png| 512]]
Fig. CloudWatch Metrics

--- 

#Question What are CloudWatch Alarms?
- CloudWatch Alarms can take actions such as Terminate EC2 Instances.
- CloudWatch Unified Agent - is an installable agent that provides a lot more metrics e.g., memory consumption, swap space
---

#Question  What are the main concepts of CloudWatch?

The following table outlines:

| Concept     | Description|
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Namespace   | A _namespace_ is a container for CloudWatch metrics.|
| Metric      | A metric represents a time-ordered set of data points that are published to CloudWatch.                                                                                                                                                                 |
| Timestamp   | Each metric data point must be associated with a time stamp in UTC - Coordinated Universal Time                                                                                                                                                         |
| Dimension   | A _dimension_ is a name/value pair that is part of the identity of a metric. You can assign up to 30 dimensions to a metric.                                                                                                                            |
| Resolution  | Granularity of metric Standard = 1 min and High = 1 sec                                                                                                                                                                                                 |
| Statistics  | _Statistics_ are metric data aggregations over specified periods of time.                                                                                                                                                                               |
| Unit        | Each statistic has a unit of measure. Example units include `Bytes`, `Seconds`, `Count`, and `Percent`.                                                                                                                                    |
| Period      | A _period_ is the length of time associated with a specific Amazon CloudWatch statistic.                                                                                                                                                                |
| Aggregation | Aggregates statistics according to the period length that you specify e.g. Web hit latency aggregation every 60 seconds                                                                                                                                 |
| Percentile  | Percentiles are often used to isolate anomalies.                                                                                                                                                                                                        |
| Alarm       | You can use an _alarm_ to automatically initiate actions on your behalf. An alarm watches a single metric over a specified time period, and performs one or more specified actions, based on the value of the metric relative to a threshold over time. |

---
### CloudWatch Canary Synthetics

#Question What is  CloudWatch Synthetics Canary?
- You can take screenshots of the UI
- Configurable script that monitors APIs and Apps/Web
- Write in Node.JS, or Python. Access headless Chrome.
- Canary Blueprint:
	- Heartbeat - load URL, store screenshot and an HTTP archive file
	- API Canary,
	- Broken Link Checker, 
	- Visual Monitoring
	- Canary Recorder
	- GUI Workflow Builder
	- 
---
### CloudWatch Integrations

#Question Which CloudWatch Integrations are supported?

| Timing         | Integration Type                      |
| -------------- | ------------------------------------- |
| Not Realtime  | S3 export is available after 12 hours |
| Near- Realtime | Kinesis Data Firehose                 |
| Realtime      | Lambda                                |

Table. _Subscriptions are filters that are applied to CloudWatch logs._ 

**CloudWatch Subscription Architecture**
![[CloudWatch Subscription Architecture.png|512]]
Fig. Subscription Filter is central to CloudWatch integrations

Lambda, Kinesis Data Streams, Kinesis Firehose, OpenSearch (Elastic Search), and S3 integrations are supported.

---

### CloudWatch Multi-Region Multi-Account

#Question How does CloudWatch support multiple accounts across multiple regions?

This is done via CloudWatch Subscription Filters.

![[Cloudwatch Multiaccount Subscription Filter Architecture.png|512]]
Fig. Subscription Filter across Regions stream to KDS then KDF for near real-time

#Question How can CPU utilization metrics from EC2 instances across instances be aggregated?

Detailed Monitoring must be enabled for aggregation.
Metric math should be used to calculate.
[CW Metrics Aggregation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/GetSingleMetricAllDimensions.html)

---

> **Hybrid and EC2 CloudWatch Architecture**
> Requires a CloudWatch Agent (only logs), new CloudWatch Unified Agent (RAM, CPU, Disk, Network is out of the box for EC2)
> ![[CloudWatch Agent Architecture.png|256]]

> **CloudWatch Alarm Targets Architecture**
> Alarms should be sent to SNS from there subscribers can take any action.
> SNS subscriber can be a Lambda function, and it can use AWS SDK to pretty much do anything with the appropriate role.

**[[EventBridge]] Enables CloudWatch Integration**

**CloudWatch Dashboard Access**
- You can create a dashboard and give access via e-mail directly from AWS Console.
- CloudWatch>Dashboard>Select your board>Share Dashboard>Share your dashboard and require a username and password>Enter email address.
- 
**CloudWatch Insights**
Operational visibility into various workloads. 

| CloudWatch Insights | #UseCase                                                                                       |
| ------------------- | --------------------------------------------------------------------------------------------- |
| Container           | Aggregate logs and metrics from containers via CloudWatch agent within EKS, ECS, K8S, Fargate |
| Lambda              | Cold starts, lambda worker shutdown.                                                          |
| Contributor         | Top-N contributors based on CloudWatch logs                                                   |
| Application         | SageMaker driven to isolate ongoing issues. EventBridge and [[SSM Parameter Store]] OpsCenter integration         |

### CloudWatch Unified Agent 

#Question: What is procstat plug-in?
**Answer**: Linux systems have /proc/stat and CW Agent can send this to CW.

#Question : How can CW use SSM Parameter Store?
**Answer**:  Install CW Unified Agent on [[EC2]] and then upon startup ensure the config is fetched from [[SSM]] parameter store: `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c ssm:AmazonCloudWatch-linux -s`


---
>  **References for CloudWatch**
	1.  https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Unified-Cross-Account.html
	2. https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html
	3. https://aws.amazon.com/about-aws/whats-new/2017/07/amazon-cloudwatch-introduces-high-resolution-custom-metrics-and-alarms/


*Created  2023-03-15 22:16*