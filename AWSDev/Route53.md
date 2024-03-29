Route53 is a **Managed DNS (Domain Name System)**, where DNS is a collection of rules and records which helps clients understand how to reach a server through URLs

In AWS, the most common records are

- A: URL to IPv4
- AAAA: URL to IPv6
- CNAME: URL to URL
- Alias: URL to AWS resource

## 1. DNS Records

| Record Type | Description                 |
| ----------- | --------------------------- |
| A           | Host Address                |
| AAAA        | IPv6 host address           |
| ALIAS       | Auto resolved alias         |
| CNAME       | Canonical name for an alias |
| MX          | Mail eXchange               |
| NS          | Name Server                 |
| PTR         | Pointer                     |
| SOA         | Start Of Authority          |
| SRV         | Location of service         |
| TXT         | Descriptive text            |

note: Elastic Load Balancers do not have pre-defined IPv4 addresses, you resolve to them using a DNS name.

What is TTL (Time-to-Live)?

It is the length that a **DNS record** is cached on

1. Resolving Server
2. User’s local PC

in *seconds*

### 1.1 Start of Authority Record (SOA)

SOA Records contains information about:

1. The name of the server that supplied the data
2. the administrator of the zone
3. The current version of the data file
4. The default number of seconds for the “time-to-live” (TTL) file on resource records

### 1.2 NS Record

NS Record stands for **Name Server Record**

They are used by top-level domain servers -> direct traffic to Content DNS Server, which contains the authoritative DNS Records

### 1.3 A Record

An “A Record” is a fundamental type of DNS Record

**A** stands for **Address**

A Record is used by a computer to translate the name of the domain to an IP Address

### 1.4 Alias Record and CName

- The

   

  CNAME record

   

  maps a URL to another URL. It should only be used when there are no other records on that name. Use a

   

  CNAME

   

  record if you want to alias one name to another name.

  - eg. `app.mydomain.com -> xxx.newdomain.com`
  - CNAME is only for NON-ROOT DOMAIN -> `something.mydomain.com`

- The

   

  ALIAS record

   

  maps a URL to an AWS Resource but can co-exist with other records on that name. Use an

   

  ALIAS record

   

  if you’re trying to alias the root domain (apex zone).

  - Works for ROOT DOMAIN and NON ROOT DOMAIN, `mydomain.com`
  - Free of charge, and native health checks
  - Alias Record is used to map resource record sets in your hosted zone to Elastic Load Balancers / CloudFront Distributions / S3 Buckets
    - it maps one DNS name to another target DNS name



## 2. Routing Policies

References: https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html

In summary:

![img](https://mk0digitalcloud3kwjy.kinstacdn.com/wp-content/uploads/2019/03/AWS-Route-53-Routing-Policies.jpg)

### 2.1 Simple Routing Policy

One record with **multiple IP addresses**. If you specify **multiple values in a record**, Route53 returns a random one which is chosen by the client

Simple Routing Policy does not support health checks

> If you choose the simple routing policy in the Route 53 console, you can’t create multiple records that have the same name and type, but you can specify multiple values in the same record, such as multiple IP addresses. (If you choose the simple routing policy for an *alias record*, you can specify only one AWS resource or one record in the current hosted zone.) If you specify multiple values in a record, Route 53 returns all values to the recursive resolver in random order, and the resolver returns the values to the client (such as a web browser) that submitted the DNS query. The client then chooses a value and resubmits the query.

### 2.2 Weighted Routing Policy

![img](https://d2908q01vomqb2.cloudfront.net/cb4e5208b4cd87268b208e49452ed6e89a68e0b8/2016/10/26/Upgrades_Image1.jpeg)

Allows you to split your traffic based on different weights assigned. For example, you can set 10% of your traffic to go to US-EAST-1 and 90% to EU-WEST-1.

You can gradually change the balance by changing the weights. If you want to stop sending traffic to a resource, you can change the weight for that record to 0.

### 2.3 Letancy Routing Policy

Allows you to route your traffic based on the lowest network latency for your end-user (ie which region will give them the fastest response time).

To use latency-based routing, we need to create a latency resource record set for EC2 or ELB resources in each region that hosts your website.

Latency-based routing is based on latency measurements performed *over a period of time*, and the measurements reflect these changes.

> Latency is evaluated in terms of the user to designated AWS Region

### 2.4 Failover Routing Policy

![img](https://miro.medium.com/max/912/1*o76vPCV2AF0jeVVunVwYDA.png)

Failover routing lets you route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy.

This is used when you want to create an active/passive setup. For example, you may want your primary site to be in EU-WEST-2 and your secondary DR Site in AP-SOUTHEAST-2. Route53 will monitor the health of your primary site using health checks.

### 2.5 Geolocation Routing Policy

![img](https://intellipaat.com/blog/wp-content/uploads/2019/05/r5.png)

Geolocation works by mapping IP addresses to locations. However, some IP addresses aren’t mapped to geographic locations, so even if you create geolocation records that cover all seven continents, Amazon Route 53 will receive some DNS queries from locations that it can’t identify. You can create a **default** record that handles both queries from IP addresses that aren’t mapped to any location and queries that come from locations that you haven’t created geolocation records for.

**If you don’t create a default record, Route 53 returns a “no answer” response for queries from those locations.**

### 2.6 Geoproximity Routing Policy (Traffic Flow Only)

Geoproximity routing lets Route53 route traffic to your resources based on the geographic location of your users and your resources. You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a bias. A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource.

### 2.7 Multivalue Answer Policy

- use when routing traffic to multiple resources
- want to associate Route53 health checks with records
- up to 8 healthy records are returned for each multi-value query
- **not a substitution for having an ELB**

It lets you configure Route53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries. You can specify multiple values for almost any record, but multivalue answer routing also lets you check the health of each resource, so Route53 returns only values for healthy resources.

Similar to simple routing but with **health checks** on each recordset

## Route53 as a Registrar (*)

A domain name registrar is an organization that manages the reservation fo Internet domain names

Route53, GoDaddy, Google Domains …

> Domain Registrar != DNS

If you buy your domain on 3rd party website, you can still use Route53

1. Create a Hosted Zone in Route53
2. Update NS Records on 3rd party website to use Route53 **name servers**