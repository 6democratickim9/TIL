# AWS CloudFront

- **Content Delivery Network (CDN)**
- Improves read performance, content is cached at the edge
- 216 point of Presence globally
- **DDoS protection, integration with Shield, AWS Web Application Firewall**
- Can **expose external HTTPS** and can talk to internal HTTPS backends

## Origins

### 	S3 bucket

- **For distributing files and caching them at the edge**
- **Enhanced security** with CloudFront Origin Access Identity (OAI)
- CloudFront can be used as an **ingress** (to upload files to S3)

### 	Custom Origin(HTTP)

- **Application Load Balancer**
- EC2 instance
- S3 website
  - (must first enable the bucket as a **static S3 website**)
- **Any HTTP backend you want**