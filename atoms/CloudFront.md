CloudFront is a Content Distribution Network (CDN) Service offered by AWS. #AWSService 

## Key Features and Limitations

#Question What is the primary mechanism of CF and what are the limitations?

As soon as the first byte arrives from the origin, CloudFront forwards the object to the user. 
CloudFront also adds the object to the cache the next time someone requests it. 
While this service is helpful for content distribution, however, for UDP and non-HTTP acceleration such as IoT this won't work. Instead, we must use [[Global Accelerator]]  if the business has more advanced use cases requiring whitelisting IP addresses, reduced latency, and performance.

![Architecture|384](https://docs.aws.amazon.com/images/AmazonCloudFront/latest/DeveloperGuide/images/how-you-configure-cf.png)
Fig. CF Conceptual Architecture

### Cache  Optimization
#Question What are the various ways in which cache can be optimized and reduce origin requests?

- Use Origin Shield. CloudFront cache (edge locations and regional edge caches) can retrieve the object from Origin Shield.

See: [CloudFront Origin Shield](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/origin-shield.html)

#Question How are regional caches and POPs used to optimize cache?

Regional Caches are larger than POPs and can hold less popular objects. This saves a trip to the origin servers and keeps objects cached closest to the customer.
- Supports 30 GB file size [limits](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html)
- You can enable geo-restrictions in CloudFront. #secure 

#Question What is the impact of the CF Price Class on latency?
- You can choose **Price Class 100**; viewers in India might experience higher latency than if you choose **Price Class 200**. #CostOptimized 

#Question What is Lambda@Edge and what is it useful for?
- Lambda@Edge with CloudFront enables a variety of ways to customize the content that CloudFront delivers. #UseCase 
- Some use cases are accelerated static site delivery, VOD, and field-level encryption.
- Jamstack site folders do not end with /index.html and a function can add this to the request.

### CloudFront Security and Protection

#Question How does CF protect origins and sites?

- CloudFront works with [[WAF]] to filter IPs. CloudFront will terminate the connection, and VPC will not see Client IPs - so [[NACL]] is not useful.
- DDOS protection due to global footprint, [[Shield | AWS Shield]] integration and [[WAF | Web Application Firewall]]
- CloudFront can use HTTPS to communicate with an Elastic Load Balancing load balancer, an Amazon EC2 instance, or another custom origin.
- CloudFront supports [[RTMP]] for Video and Audio streaming. A CloudFront distribution is either a Web Distribution or an RTMP distribution but not both.

#Question How does CloudFront communicate with S3 Website Endpoint when Users connect to CloudFront with HTTPS?

If your Amazon S3 bucket is configured as a website endpoint, you can't configure CloudFront to use HTTPS to communicate with your origin because Amazon S3 doesn't support HTTPS connections in that configuration.
See: [AWS DG](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-cloudfront-to-s3-origin.html)

### CloudFront Signed URLs
- Trusted Key Group (recommended)
- AWS Account with CloudFront Key Pair (Not recommended)
	- Need to manage keys using the root account and the AWS Console
### CloudFront Field Level Encryption
- Asymmetric encryption for up to 10 fields. CloudFront will use Public Key. The private key can be used by the back-end application server or db.
### CloudFront HA
Set up an Origin Group with Primary and Secondary Origins. #Resilient 
You can set up CloudFront with origin failover for scenarios that require high availability. To get started, you create an _origin group_ with two origins: a primary and a secondary. If the primary origin is unavailable or returns specific HTTP response status codes that indicate a failure, CloudFront automatically switches to the secondary origin.

### CloudFront Functions
- Regional Edge Cache runs within 13 AWS Regions.
![[CloudFront Functions Architecture.png|128]]
Fig. Conceptual Architecture
- Edge Locations are 255 data centers across 47 countries (2022) that run limited AWS Services e.g. S3, AWS Shield, Route 53 etc.
- Files as large as 20 GB can be delivered.
- CloudFront functions are constrained JavaScript functions executed before the request hits the cache. 
![CloudFront Functions Architecture|256](https://miro.medium.com/v2/resize:fit:1400/0*feB6kqJ_WjWbpggD)
- Native feature of CloudFront Functions
- Constraints
	- No access to Internet
	- No use of await async
	- No access to file system
	- The date function returns the same time i.e. time of execution start
	- Size of code is limited to 10 KB
Some of these constraints are lifted when using [[Lambda#Lambda@Edge]]
#UseCase  Managing CORS, CSP, X-Frame-Options, and other Security HTTP Headers, Modifying the CloudFront Cache Key e.g., normalization, Redirecting Traffic Based on Simple Conditions and URL Rewrites and redirection.

---
#### Cookies and Request Parameter
#Question How are Cookies and Request Parameters handled by CloudFront?
See: [Cookies in CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Cookies.html)
**Answer**: By default, these are ignored. However a whitelist of cookies and request parameters can be specified, and for each, these will be treated as unique for caching.

---

#### ALB Sticky Session 
#Question How does CloudFront handle sticky sessions for [[ALB]] ?
See:
**Answer**: Whitelist the session cookie name to create uniqueness `AWSALB`. Use TTL for less than the authorization timeout.

---

#### CloudFront Reports

#Question What information can be gleaned from CloudFront reports for distribution?

The
1. Usage: Number of requests, data transferred.
2. Cache: HTTP Status codes, bytes transferred.
3. Popular: Top 50 objects
4. Viewer: Devices, locations
5. Top Referrer: Top 25 referrers

See: [CloudFront Reports](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/reports.html#reports-overview-viewers)

### Solution Architectures

#### On-premises server requires a global distribution
[[Hybrid Cloud Architecture]] with CloudFront is possible. A custom origin can point to an on-premises server, and CloudFront is able to cache content for dynamic websites. CloudFront can provide performance optimizations for custom origins even running on on-premises servers. These include persistent TCP connections to the origin, SSL enhancements such as Session tickets, and [[OCSP]] stapling. #performant 
Additionally, connections are routed from the nearest Edge Location to the user across the AWS global network. This can further improve performance if the on-premises server is connected via a [[DX|Direct Connect]]  link.

#Question  What is a fast and cost-efficient solution that will update the images immediately without waiting for the object’s expiration date?
**Answer**: Use different names for assets by version number e.g. `img_2023083290.jpg`. Cache-Invalidation is time-consuming and not recommended.  

---

#Question What does TTL of 0 achieve?
Answer: All requests are directed to the origin. This can be useful for 3-tier Applications that require reduced latency for users because traversal from CloudFront to origin is faster.

## References

1. [CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)
2. https://medium.com/trackit/cloudfront-functions-vs-lambda-edge-which-one-should-you-choose-c88527647695
3. https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html