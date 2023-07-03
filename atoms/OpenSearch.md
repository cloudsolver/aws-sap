Amazon OpenSearch is a successor to Amazon ElasticSearch. #AWSService 

[OpenSearch](https://aws.amazon.com/opensearch-service/) Interactive Log Analytics

* Search petabytes of unstructured data.
* Open source Elastic Search, Open Search Dashboard, and Kibana.
* Partial matches on any fields searched.
* Requires a cluster of instances (not serverless).
* Does NOT support SQL (uses proprietary query language).
* Has dashboards out of the box.
* Data ingress: [[Kinesis]] Firehose, [[IoT]], [[CW]] logs.
* Security: [[Cognito]], [[IAM]], [[KMS]] and support [[TLS]].

#Question What is a production infrastructure design for OpenSearch?

Use three masters across 3 AZs: primary and two secondaries (medium). Two data nodes per AZ (large).
![[Open Search Architecture.png]]
Fig. Open Search Architecture: 1 Active, 2 Backups for Master Nodes.